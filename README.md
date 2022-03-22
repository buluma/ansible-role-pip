# [pip](#pip)

Pip (Python package manager) for Linux.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/buluma/ansible-role-pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-pip/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-pip/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-pip)|[![quality](https://img.shields.io/ansible/quality/54591)](https://galaxy.ansible.com/buluma/pip)|[![downloads](https://img.shields.io/ansible/role/d/54591)](https://galaxy.ansible.com/buluma/pip)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-pip.svg)](https://github.com/buluma/ansible-role-pip/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: true

  vars:
    pip_install_packages:
      # Test installing a specific version of a package.
      - name: ipaddress
        version: "1.0.18"
      # Test installing a package by name.
      - colorama

  pre_tasks:
    - name: Update apt cache.
      apt: update_cache=true cache_valid_time=600
      when: ansible_os_family == 'Debian'

    - name: Set package name for older OSes.
      set_fact:
        pip_package: python-pip
      when: >
        (ansible_os_family == 'RedHat') and (ansible_distribution_major_version | int < 8)
        or (ansible_distribution == 'Debian') and (ansible_distribution_major_version | int < 10)
        or (ansible_distribution == 'Ubuntu') and (ansible_distribution_major_version | int < 18)
  roles:
    - role: buluma.pip
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for ansible-role-pip
# For Python 3, use python3-pip.
pip_package: python3-pip
pip_executable: "{{ 'pip3' if pip_package.startswith('python3') else 'pip' }}"

pip_install_packages: []
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-pip/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.co.ke/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-pip/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|el|all|
|fedora|all|
|debian|all|
|ubuntu|all|

The minimum version of Ansible required is 2.4, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-pip/issues)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[buluma](https://buluma.github.io/)
