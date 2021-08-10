# [Ansible Galaxy](https://docs.ansible.com/ansible/latest/galaxy/user_guide.html#finding-collections-on-galaxy)


## Requirements

You can install multiple roles by including the roles in a requirements.yml file. The format of the file is YAML, and the file extension must be either .yml or .yaml.

Use the following command to install roles included in requirements.yml:

```shell
ansible-galaxy install -r requirements.yml
```

```yaml
---
roles:
  # Install a role from Ansible Galaxy.
  - name: geerlingguy.java
    version: 1.9.6

collections:
  # Install a collection from Ansible Galaxy.
  - name: geerlingguy.php_roles
    version: 0.9.3
    source: https://galaxy.ansible.com
```

## Install Role

`ansible-galaxy install namespace.role_name`

## Install Collection

```shell
# Install a collection in a repository using the latest commit on the branch 'devel'
ansible-galaxy collection install git+https://github.com/organization/repo_name.git,devel

# Install a collection from a private github repository
ansible-galaxy collection install git@github.com:organization/repo_name.git

# Install a collection from a local git repository
ansible-galaxy collection install git+file:///home/user/path/to/repo/.git
```

