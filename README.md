openssh
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-openssh.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-openssh)

Install and configure openssh on your system.

Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.openssh
```

The machine you are running this on, may need to be prepared. Tests have been done on machines prepared by this playbook:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - robertdebock.bootstrap
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for openssh

# The tcp port ssh should listen on.
openssh_port: 22

openssh_address_family: any

openssh_listen_address:
  - '0.0.0.0'
  - '::'

openssh_host_key:
  - /etc/ssh/ssh_host_rsa_key
  - /etc/ssh/ssh_host_ecdsa_key
  - /etc/ssh/ssh_host_ed25519_key

openssh_rekey_limit: default none

# openssh_syslog_facility can be AUTH or AUTHPRIV
openssh_syslog_facility: AUTHPRIV

openssh_loglevel: INFO

openssh_login_grace_time: 2m
openssh_permit_root_login: "yes"
openssh_scrict_modes: "yes"
openssh_max_auth_tries: 6
openssh_max_sessions: 10

openssh_pub_key_authentication: "yes"

openssh_authorized_key_file: .ssh/authorized_keys

openssh_authorized_prinicpals_file: none
openssh_authorized_keys_command: none
openssh_authorized_keys_command_user: nobody

openssh_host_based_authentication: "no"
openssh_ignore_user_known_hosts: "no"
openssh_ignore_rhosts: "yes"

openssh_permit_empty_passwords: "no"
openssh_password_authentication: "yes"

openssh_challenge_response_authentication: "no"

openssh_gssapi_authentication: "yes"
openssh_gssapi_cleanup_credentials: "no"
openssh_gssapi_strict_acceptor_check: "yes"
openssh_gssapi_key_exchange: "no"
openssh_gssaip_enable_k5_users: "no"

openssh_use_pam: "yes"

openssh_allow_agent_forwarding: "yes"
openssh_allow_tcp_forwarding: "yes"
openssh_gateway_ports: "no"
openssh_x11_forwarding: "yes"
openssh_x11_display_offset: 10
openssh_x11_use_localhost: "yes"
openssh_permit_tty: "yes"

openssh_print_motd: "no"

openssh_print_last_log: "yes"
openssh_tcp_keep_alive: "yes"
openssh_permit_user_environment: "no"
openssh_compression: delayed
openssh_client_alive_interval: 30
openssh_client_alive_count_max: 3
openssh_show_patch_level: "no"
openssh_use_dns: "no"
openssh_pid_file: /var/run/sshd.pid
openssh_max_startups: 10:30:100
openssh_permit_tunnel: "no"
openssh_chroot_directory: none
openssh_version_addendum: none

openssh_banner: none

openssh_accept_env:
  - LANG
  - LANGUAGE
  - LC_ADDRESS
  - LC_ALL
  - LC_COLLATE
  - LC_CTYPE
  - LC_IDENTIFICATION
  - LC_MEASUREMENT
  - LC_MESSAGES
  - LC_MONETARY
  - LC_NAME
  - LC_NUMERIC
  - LC_PAPER
  - LC_TELEPHONE
  - LC_TIME
  - XMODIFIERS

openssh_subsystem: sftp /usr/libexec/openssh/sftp-server
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/openssh.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes*|
|alpine-latest|yes|yes|yes*|
|archlinux|yes|yes|yes*|
|centos-6|yes|yes|yes*|
|centos-latest|yes|yes|yes*|
|debian-latest|yes|yes|yes*|
|debian-stable|yes|yes|yes*|
|debian-unstable*|yes|yes|yes*|
|fedora-latest|yes|yes|yes*|
|fedora-rawhide*|yes|yes|yes*|
|opensuse-leap|yes|yes|yes*|
|ubuntu-devel*|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes*|
|ubuntu-rolling|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-openssh) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-openssh/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

Run the [ansible-galaxy](https://github.com/ansible/galaxy-lint-rules) and [my](https://github.com/robertdebock/ansible-lint-rules) lint rules if you want your change to be merges:

```shell
git clone https://github.com/ansible/ansible-lint.git /tmp/ansible-lint
ansible-lint -r /tmp/ansible-lint/lib/ansiblelint/rules .

git clone https://github.com/robertdebock/ansible-lint /tmp/my-ansible-lint
ansible-lint -r /tmp/my-ansible-lint/rules .
```

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
