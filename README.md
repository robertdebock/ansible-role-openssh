# openssh

Install and configure openssh on your system.

|Travis|GitHub|Quality|Downloads|
|------|------|-------|---------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-openssh.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-openssh)|[![github](https://github.com/robertdebock/ansible-role-openssh/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-openssh/actions)|[![quality](https://img.shields.io/ansible/quality/30937)](https://galaxy.ansible.com/robertdebock/openssh)|[![downloads](https://img.shields.io/ansible/role/d/30937)](https://galaxy.ansible.com/robertdebock/openssh)|

## Example Playbook

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.openssh
```

The machine may need to be prepared using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - robertdebock.bootstrap
```

For verification `molecule/resources/verify.yml` run after the role has been applied.
```yaml
---
- name: Verify
  hosts: all
  become: yes
  gather_facts: yes

  tasks:
    - name: check if connection still works
      ping:
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## Role Variables

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

## Requirements

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap

```

## Context

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/openssh.png "Dependency")

## Compatibility

This role has been tested on these [container images](https://hub.docker.com/):

|container|tags|
|---------|----|
|amazon|all|
|alpine|all|
|debian|all|
|el|7, 8|
|fedora|all|
|opensuse|all|
|ubuntu|bionic|

The minimum version of Ansible required is 2.8 but tests have been done to:

- The previous version, on version lower.
- The current version.
- The development version.



## Testing

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-openssh) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-openssh/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## License

Apache-2.0


## Author Information

[Robert de Bock](https://robertdebock.nl/)
