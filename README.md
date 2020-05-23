# Ansible Role: Common

![Build Status](https://github.com/vladgh/ansible-role-common/workflows/CI/badge.svg)

Vlad's Common Ansible Role.

## Requirements

*_N/A_*

## Role Variables

Available variables are listed below, along with default values (see defaults/main.yml):

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

### CloudFlare DNS

Check <https://docs.ansible.com/ansible/latest/modules/cloudflare_dns_module.html> for a complete list of parameters

```yaml
cloudflare_email: "{{ vault_cloudflare_email }}"
cloudflare_api_token: "{{ vault_cloudflare_api_token }}"
cloudflare_dns_records:
  - zone: example.com
    type: A
    record: test
    value: 192.168.1.2
```

### CRON Jobs

Check <https://docs.ansible.com/ansible/latest/modules/cron_module.html> for a complete list of parameters

```yaml
cron_jobs:
  - name: Docker CleanUp
    minute: '2'
    hour: '2'
    job: docker system prune --force 2>&1 | /usr/bin/logger -t DockerCleanUp
```

### Remote logging

- `remote_logs_enabled`: Set to true to enable remote logging (defaults to `false`)
- `remote_logs_server`: Remote logs server (defaults to `logs.example.com`)
- `remote_logs_port`: Remote logs port (defaults to `10514`)
- `remote_logs_protocol`: Remote logs protocol (defaults to `tcp`)

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

### Additional packages

- `additional_packages`: A list of packages to install using APT/YUM

## Dependencies

*_N/A_*

## Example Playbook

```yaml
- hosts: all
  become: yes
  roles:
      - vladgh.common
```

## Contribute

See [CONTRIBUTING.md](CONTRIBUTING.md) file.

## License

Licensed under the Apache License, Version 2.0.
See [LICENSE](LICENSE) file.
