zabbix_web
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-zabbix_web"><img src="https://travis-ci.org/robertdebock/ansible-role-zabbix_web.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure zabbix_web on your system.

<img src="https://img.shields.io/ansible/role/d/35789"/>
<img src="https://img.shields.io/ansible/quality/35789"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.zabbix_web
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.epel
    - role: robertdebock.buildtools
    - role: robertdebock.python_pip
    - role: robertdebock.zabbix_repository
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for zabbix_web

# Details to connect to the database.
zabbix_web_database_host: localhost
zabbix_web_database_port: 3306
zabbix_web_database_name: zabbix
zabbix_web_database_user: zabbix
zabbix_web_database_pass: zabbix

# Details to connect to Zabbix.
zabbix_web_server: https://localhost/zabbix
zabbix_web_server_port: 10051
zabbix_web_server_name: zabbix

# Details to connect to the Zabbix API.
zabbix_web_username: Admin
zabbix_web_password: zabbix
zabbix_web_validate_certs: no

# You can provision Zabbix groups.
# Most options map directly to the documentation:
# https://docs.ansible.com/ansible/latest/modules/zabbix_group_module.html
zabbix_web_groups:
  - name: Linux servers

# Add hosts to Zabbix.
# Most options map directly to the documentation:
# https://docs.ansible.com/ansible/latest/modules/zabbix_host_module.html
zabbix_web_hosts:
  - name: Example server 1
    interface_ip: 192.168.127.127
    interface_dns: server1.example.com
    visible_name: Example server 1 name
    description: Example server 1 description
    groups:
      - Linux servers
    link_templates:
      - Template OS Linux
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.epel
- robertdebock.buildtools
- robertdebock.python_pip
- robertdebock.zabbix_repository

```

This role uses the following modules:
```yaml
---
- meta
- package
- pip
- service
- template
- zabbix_group
- zabbix_host
```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/zabbix_web.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tag|allow_failures|
|---------|---|--------------|
|debian|stable|yes|
|debian|unstable|yes|
|debian|latest|no|
|centos|7|no|
|centos|latest|no|
|ubuntu|rolling|yes|
|ubuntu|devel|yes|
|ubuntu|latest|no|

This role has been tested on these Ansible versions:

- ansible~=2.7
- ansible~=2.8
- git+https://github.com/ansible/ansible.git@devel

The indicator '\~=' means [compatible with](https://www.python.org/dev/peps/pep-0440/#compatible-release). For example 'ansible\~=2.8' would pick the latest ansible-2.8, for example ansible-2.8.6.

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Archlinux | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| CentOS 8 | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Debian | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Fedora | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| openSUSE | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Ubuntu rolling | Zabbix has [limited OS support](https://www.zabbix.com/download). |



Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-zabbix_web) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-zabbix_web/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
