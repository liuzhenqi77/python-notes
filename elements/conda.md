# Conda

## Command Line Utilities

```bash
# show conda version
conda --version

# update conda to current version
conda update conda
```

```bash
# create new environment
conda create --name ENV_NAME python=3.6 numpy scipy matplotlib
```

To enter a environment, use `activate ENV_NAME` on Windows and `source activate ENV_NAME` on Ubuntu.

To leave, use `deactivate` on Windows and `source deactivate` on Ubuntu.

```bash
# list all environments
conda info --envs

conda env list

conda env remove --name ENV_NAME
```

```bash
conda search PACKAGE_NAME

conda install PACKAGE_NAME

conda update PACKAGE_NAME

conda list
```

After installation a package in your environment, like `jupyter`, you can start it by run `jupyter` from the command line.

You can also use `pip` to install packages, which will show its source from `<pip>`.

## Config with `.condarc`

The configuration file `.condarc` is typically located in user home or root directory, like `~/.condarc` on Ubuntu or `C:\Users\%USERNAME%` on Windows. On the first run, you can either create a txt file (save without extension name), or run `conda config`.

Here is a sample config file used by myself. It contains the following features:

- custom channels
  - defaults: for the default channel (slow in China)
  - conda-forge: for in-dev packages
  - tsinghua-tuna mirror: fast mirror (especially for Education Network users)
- proxy server setting if you prefer the default channel

```bash
# channel locations. These override conda defaults, i.e., conda will
# search *only* the channels listed here, in the order given.
# Use "defaults" to automatically include all default channels.
# Non-url channels will be interpreted as Anaconda.org usernames
# (this can be changed by modifying the channel_alias key; see below).
# The default is just 'defaults'.
channels:
  - defaults
  - conda-forge
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

# Show channel URLs when displaying what is going to be downloaded
# and in 'conda list'. The default is False.
show_channel_urls: yes

# Set proxy servers
proxy_servers:
  http: 127.0.0.1:1080
ssl_verify: true
```