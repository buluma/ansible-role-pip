# [pip](#pip)

Install Pip (Python package manager) for Linux.

|GitHub|GitLab|Downloads|Version|Issues|Pull Requests|
|------|------|-------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-pip/actions)|[![gitlab](https://gitlab.com/shadowwalker/ansible-role-pip/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-pip)|[![downloads](https://img.shields.io/ansible/role/d/4802)](https://galaxy.ansible.com/buluma/pip)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-pip.svg)](https://github.com/buluma/ansible-role-pip/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-pip.svg)](https://github.com/buluma/ansible-role-pip/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-pip.svg)](https://github.com/buluma/ansible-role-pip/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-pip/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

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
    - name: update apt cache.
      apt: update_cache=true cache_valid_time=600
      when: ansible_os_family == 'Debian'

    - name: set package name for older OSes.
      set_fact:
        pip_package: python-pip
      when: >
        (ansible_os_family == 'RedHat') and (ansible_distribution_major_version | int < 8)
        or (ansible_distribution == 'Debian') and (ansible_distribution_major_version | int < 10)
        or (ansible_distribution == 'Ubuntu') and (ansible_distribution_major_version | int < 18)
  roles:
    - role: buluma.pip
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-pip/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  become_method: su
  gather_facts: false
  vars:
    ansible_python_interpreter: /usr/bin/python3

  roles:
    - role: buluma.bootstrap
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-pip/blob/master/defaults/main.yml):

```yaml
---
# For Python 3, use python3-pip.
pip_package: python3-pip
pip_executable: "{{ 'pip3' if pip_package.startswith('python3') else 'pip' }}"

pip_install_packages: []
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-pip/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Build Status GitHub](https://github.com/buluma/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.setuptools](https://galaxy.ansible.com/buluma/setuptools)|[![Build Status GitHub](https://github.com/buluma/ansible-role-setuptools/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-setuptools/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-setuptools/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-setuptools)|
|[buluma.openssl](https://galaxy.ansible.com/buluma/openssl)|[![Build Status GitHub](https://github.com/buluma/ansible-role-openssl/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-openssl/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-openssl/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-openssl)|
|[buluma.ca_certificates](https://galaxy.ansible.com/buluma/ca_certificates)|[![Build Status GitHub](https://github.com/buluma/ansible-role-ca_certificates/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-ca_certificates/actions)|[![Build Status GitLab](https://gitlab.com/shadowwalker/ansible-role-ca_certificates/badges/master/pipeline.svg)](https://gitlab.com/shadowwalker/ansible-role-ca_certificates)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-pip/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|8|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|all|
|[Kali](https://hub.docker.com/repository/docker/buluma/kali/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-pip/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-pip/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-pip/blob/master/LICENSE).

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)

Please consider [sponsoring me](https://github.com/sponsors/buluma).

### [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
