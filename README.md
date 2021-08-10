# ansible-toolbox

## Table of contents

- [ansible-toolbox](#ansible-toolbox)
  - [Table of contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
    - [Install python](#install-python)
    - [Install pip](#install-pip)
    - [Installation with pip](#installation-with-pip)
    - [Install Ansible in a virtual environment with pip](#install-ansible-in-a-virtual-environment-with-pip)
    - [Installation on Ubuntu](#installation-on-ubuntu)
    - [Install python on remote hosts](#install-python-on-remote-hosts)
  - [Ansible Config](#ansible-config)
  - [Command Line](#command-line)
    - [ansible-playbook](#ansible-playbook)
      - [Most used options](#most-used-options)
  - [Yaml Syntax](#yaml-syntax)
    - [List](#list)
    - [Dictionnary](#dictionnary)

## [Prerequisites](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#prerequisites)

**Starting with version 2.10, Ansible distributes two artifacts: a community package called ansible and a minimalist language and runtime called ansible-core (called ansible-base in version 2.10)**

- python
- pip
- [Windows host](https://docs.ansible.com/ansible/latest/user_guide/windows_setup.html#setting-up-a-windows-host)

## Installation

### [Install python](https://docs.python.org/fr/3/using/unix.html#on-linux)

```shell
    sudo apt-get install software-properties-common
    sudo add-apt-repository ppa:deadsnakes/ppa
    sudo apt-get update
    sudo apt-get install python3.9 `
```

### Install pip

```shell
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
    python get-pip.py --user 
```



### [Installation with pip](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-and-upgrading-ansible-with-pip)

``` shell
    sudo python get-pip.py
    sudo python -m pip install ansible
```

### Install Ansible in a virtual environment with pip

```shell
    python -m virtualenv ansible  # Create a virtualenv if one does not already exist
    source ansible/bin/activate   # Activate the virtual environment
    python -m pip install ansible
```

### [Installation on Ubuntu](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-ubuntu)

**Ansible > 2.10 only available through pip**

```shell
    sudo apt update
    sudo apt install software-properties-common
    sudo add-apt-repository --yes --update ppa:ansible/ansible
    sudo apt install ansible
```

### [Install python on remote hosts](https://blog.knoldus.com/how-to-install-python-in-target-host-using-ansible/)

Ansible’s raw module, and the script module, do not depend on a client side install of Python to run. Technically, you can use Ansible to install a compatible version of Python using the raw module, which then allows you to use everything else. For example, if you need to bootstrap Python 2 onto a RHEL-based system, you can install it as follows:

`ansible myhost --become -m raw -a "yum install -y python3"`

```ansible
- name: Bootstrap a host without python2 installed
  raw: dnf install -y python2 python2-dnf libselinux-python
```

## Ansible Config

Priority order for config:

1. /etc/ansible/ansible.cfg
2. [~/.ansible.cfg](.ansible.cfg)
3. ansible.cfg in the working directory
4. Environment variables (eg: ANSIBLE_CONFIG) 
5. CLI


## [Command Line](https://docs.ansible.com/ansible/latest/user_guide/command_line_tools.html#working-with-command-line-tools)

- ansible
- ansible-config
- ansible-console
- ansible-doc
- ansible-galaxy
- ansible-inventory
- ansible-playbook
- ansible-pull
- ansible-vault

### [ansible-playbook](https://docs.ansible.com/ansible/latest/cli/ansible-playbook.html)

``` ansible
usage: ansible-playbook [-h] [--version] [-v] [-k]
                     [--private-key PRIVATE_KEY_FILE] [-u REMOTE_USER]
                     [-c CONNECTION] [-T TIMEOUT]
                     [--ssh-common-args SSH_COMMON_ARGS]
                     [--sftp-extra-args SFTP_EXTRA_ARGS]
                     [--scp-extra-args SCP_EXTRA_ARGS]
                     [--ssh-extra-args SSH_EXTRA_ARGS] [--force-handlers]
                     [--flush-cache] [-b] [--become-method BECOME_METHOD]
                     [--become-user BECOME_USER] [-K] [-t TAGS]
                     [--skip-tags SKIP_TAGS] [-C] [--syntax-check] [-D]
                     [-i INVENTORY] [--list-hosts] [-l SUBSET]
                     [-e EXTRA_VARS] [--vault-id VAULT_IDS]
                     [--ask-vault-password | --vault-password-file VAULT_PASSWORD_FILES]
                     [-f FORKS] [-M MODULE_PATH] [--list-tasks]
                     [--list-tags] [--step] [--start-at-task START_AT_TASK]
                     playbook [playbook ...]
```

#### Most used options

- **-C, --check** : don’t make any changes; instead, try to predict some of the changes that may occur
- **-D, --diff** : when changing (small) files and templates, show the differences in those files; works great with –check
- **-i, --inventory, --inventory-file** : specify inventory host path or comma separated host list. –inventory-file is deprecated
- **-t, --tags** : only run plays and tasks tagged with these values

## [Yaml Syntax](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html)

### List

```yaml
---
# A list of tasty fruits
- Apple
- Orange
- Strawberry
- Mango
...
```

### Dictionnary

```yaml
# An employee record
martin:
  name: Martin D'vloper
  job: Developer
  skill: Elite
```