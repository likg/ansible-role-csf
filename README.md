[![Ansible Galaxy](https://img.shields.io/badge/role-likg.csf-blue.svg?style=flat)](https://galaxy.ansible.com/likg/csf/)
[![Build Status](https://travis-ci.org/likg/ansible-role-csf.svg?branch=master)](https://travis-ci.org/likg/ansible-role-csf)

# Ansible Role: CSF/LFD

Install and configure [CSF/LFD](https://configserver.com/cp/csf.html)

## Requirements

CSF/LFD is a set of perl scripts, thus perl interpreter is required. Many popular distros comes with perl installed by default, nevertheless, this role will install perl if it is missing.

Full list of required packages (will be installed by this role) defined in [`csf_required_packages`](defaults/main.yml#L6-L11) and [`csf_required_packages_dist`](vars/) variables.

## Role Variables

Available variables with their default values can be found in [defaults/main.yml](defaults/main.yml).

## Dependencies

None.

## Example Playbook
```yaml
- hosts: servers
  become: yes
  roles:
    - { role: likg.csf }
  vars_files:
    - path_to_vars.yml
```

File `path_to_vars.yml`:
```yaml
csf_global_ini:
  - option: RESTRICT_SYSLOG
    value: "2"
  - option: URLGET
    value: "2"
  - option: TCP_IN
    value: "80,443,{{ hostvars[inventory_hostname]['ansible_port'] | default('22') }},30000:65535"
  - option: TCP_OUT
    value: "20,21,22,25,37,43,53,80,123,443,873,953,8080,9418,{{ hostvars[inventory_hostname]['ansible_port'] | default('22') }},30000:65535"
  - option: UDP_IN
    value: "53"
  - option: UDP_OUT
    value: "20,21,43,53,113,123,58745,30000:65535"

csf_allow:
  - 10.10.10.10
  - 172.16.1.1/29

csf_ignore:
  - 10.10.10.10
  - 172.16.1.1/29

csf_pignore:
  - 'exe:/usr/sbin/nginx'
  - 'user:mysql'

csf_fignore:
  - '/tmp/\.horde'
  - '/tmp/\.horde/.*'

csf_blocklists:
  - "SPAMDROP"

csf_csfpre_sh: |
  #!/bin/bash
  /sbin/iptables -t nat -F POSTROUTING
```
## License

MIT

## Author Information

This role was created by Lik.
