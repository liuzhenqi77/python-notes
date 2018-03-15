# Logging

See end of this page for complete recipe.

## Full Recipe

### Usage

```python
import logging
logger = configure_logger(__name__, log_file_name)
logger.debug()
logger.info()
logger.warning()
logger.error()
logger.critical()
```
### Utility Code

```python
class word_filter(logging.Filter):
    """
    This is a auxillary class for function configure_logger()
    Defines a logging.Filter tool to filter certain words from the log
    Use record.property to access the log and self.param to store a black list
    """
    def __init__(self, param=None):
        self.param = list(param)

    def filter(self, record):
        if self.param is None:
            allow = True
        else:
            allow = not any(_ in record.name for _ in self.param)
        # if allow:
            # record.msg = 'changed: ' + record.msg
        return allow


def configure_logger(name, log_path):
    """custom logger
    This is a custom logger tuned for best debugging.
    Please also include the word_filter class above.
    :param name: name to show in the log
    :param log_path: path to save the log file
    :return:
    """
    logging.config.dictConfig({
        'version': 1,
        'disable_existing_loggers': False,
        'formatters': {
            'default': {
                'format': '[%(asctime)s][%(levelname)s][%(name)s][%(funcName)s():%(lineno)s] - %(message)s',
                'datefmt': '%Y-%m-%d %H:%M:%S'
            }
        },
        'filters': {
            'word_filter': {
                '()': word_filter,
                'param': ['PIL'],
            }
        },
        'handlers': {
            'console': {
                'level': 'INFO',
                'filters': ['word_filter'],
                'class': 'logging.StreamHandler',
                'formatter': 'default'
            },
            'file': {
                'level': 'DEBUG',
                'filters':['word_filter'],
                'class': 'logging.handlers.RotatingFileHandler',
                'formatter': 'default',
                'filename': log_path,
                'mode': 'w',
                'backupCount': 3
            }
        },
        'loggers': {
            '': {
                'level': 'DEBUG',
                'handlers': ['console', 'file'],
                'propagate': True
            }
        }
    })
    return logging.getLogger(name)
```
