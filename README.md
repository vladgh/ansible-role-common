# Ansible Role: Common

[![Build Status](https://travis-ci.com/vladgh/ansible-role-common.svg?branch=master)](https://travis-ci.com/vghn/ansible-role-common)

Vlad's Common Ansible Role.

## Requirements

*N/A*

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

### Essential packages

- `debian_software`: A list of packages to install using APT
- `redhat_software`: A list of packages to install using YUM

### User accounts

Check <https://docs.ansible.com/ansible/latest/modules/user_module.html> for a complete list of parameters

```yaml
accounts:
  - name: username
    comment: My User Name
    uid: 8888
    groups: admins
    append: yes
    shell: /bin/bash
    authorized_keys:
      - ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIE0yyqRUbBGOW9PcYyuaUMaRi/EFwL59E3wwMn5dJAKQ MyKey
```

### Extra APT repositories on Debian systems

Check <https://docs.ansible.com/ansible/latest/modules/apt_repository_module.html> for a complete list of parameters

```yaml
apt_repositories:
  - name: GIT
    repo: ppa:git-core/ppa
```

### Remote logging

- `remote_logs_enabled`: Set to true to enable remote logging (defaults to `false`)
- `remote_logs_server`: Remote logs server (defaults to `logs.example.com`)
- `remote_logs_port`: Remote logs port (defaults to `10514`)
- `remote_logs_protocol`: Remote logs protocol (defaults to `tcp`)

### MSMTP relay

- `msmtp_enabled`: Set to true to enable MSMTP relay (defaults to `false`)
- `msmtp_log`: Log type; one of `syslog`, `file` or `no` (defaults to `syslog`)
- `msmtp_logfile`: If above type is file, the path to it (defaults to `/var/log/msmtp.log`)
- `msmtp_accounts`: A hash of MSMTP accounts, for example

    ```yaml
    - account: mysmtp
      host: smtp.example
      port: 587
      auth: on
      from: me
      user: myuser
      password: 123456
    ```

- `msmtp_default_account`: Default MSMTP account from the list above
- `msmtp_alias_default`: The default user alias (defaults to `root`)
- `msmtp_alias_root`: The root alias (defaults to `msmtp_alias_default`)
- `msmtp_alias_cron`: The cron alias (defaults to `msmtp_alias_default`)
- `msmtp_ca_certificates_bundle`: The path for the certificates bundle (default to system's CA Certificates Paths; see `vars/OS_FAMILY.yml`)

### Extra mount points

Check <https://docs.ansible.com/ansible/latest/modules/mount_module.html> for a complete list of parameters

```yaml
mount_points:
  - name: MyBackup
    path: /data/backup
    src: UUID=1234-1234-1234-1234-1234
    fstype: ext4
    state: mounted
```

### Miscellaneous

- `disable_lid_switch`: Set to true to disable lid switch on laptops (defaults to `false`)

## Dependencies

*N/A*

## Example Playbook

```yaml
- hosts: all
  become: yes
  roles:
      - vladgh.common
```

## License

Apache License 2.0

## Author Information

Vlad Ghinea - <https://ghn.me>
