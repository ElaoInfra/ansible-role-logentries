<img src="http://www.elao.com/images/corpo/logo_red_small.png"/>

# Ansible Role: logentries

This role will assume the setup of logentries

It's part of the ELAO [Ansible stack](http://ansible.elao.com) but can be used as a stand alone component.

## Requirements

- Ansible 1.7.2+

## Dependencies

None.

## Installation

Using ansible galaxy:

```bash
ansible-galaxy install elao.logentries
```
You can add this role as a dependency for other roles by adding the role to the meta/main.yml file of your own role:

```yaml
dependencies:
  - { role: elao.logentries }
```

## Role Handlers

| Name                 | Type    | Description              |
| -------------------- | ------- | ------------------------ |
| `logentries restart` | Service | Restart logentries agent |

## Role Variables

| Name                              | Default                     | Type   | Description          |
| ----------------------------      | --------------------------- | ------ | -------------------- |
| `elao_logentries_config_template` | config/default.j2           | String | Main config template |
| `elao_logentries_config_file`     | /etc/le/config              | String | Main config file     |
| `elao_logentries_config`          | {}                          | Array  | Main config          |

### Configuration example

```yaml
elao_logentries_config:
  - Main:
    - 'pull-server-side-config': 'False'
  - 'nginx-access':
    - path: /var/log/nginx/access.log
    - token: "{{ _logentries_nginx_access_token }}"
  - 'nginx-error':
    - path: /var/log/nginx/error.log
    - token: "{{ _logentries_nginx_error_token }}"
```

## Example playbook

    - hosts: servers
      roles:
         - { role: elao.logentries }

# Licence

MIT

# Author information

ELAO [**(http://www.elao.com/)**](http://www.elao.com)
