# Ansible Role: CSF/LFD

Install and configure [CSF/LFD](https://configserver.com/cp/csf.html)

## Requirements

No special requirements.

## Role Variables

Available variables/default values can be found in [defaults/main.yml](defaults/main.yml).

## Dependencies

None.

## Example Playbook

    - hosts: servers
      become: yes
      vars:
        - csf_pignore_extra: ["exe:/usr/sbin/httpd", "exe:/usr/lib64/icinga2/sbin/icinga2"]
      roles:
        - { role: likg.csf }

## License

MIT

## Author Information

This role was created by Lik.