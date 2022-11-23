# systemd service manager Ansible role

This is an [Ansible](https://www.ansible.com/) role which manages systemd services.


## Features

- **starting** (restarting) services, in order, according to their `priority`

- making services **auto-start** (see `devture_systemd_service_manager_services_autostart_enabled`)

- **verifying** start services managed to start (see `devture_systemd_service_manager_up_verification_enabled`)

- **stopping** services, in order, according to their `priority`


## Usage

Example playbook:

```yaml
- hosts: servers
  roles:
    - when: devture_systemd_service_manager_enabled | bool
      role: galaxy/com.devture.ansible.role.systemd_service_manager
```

Example playbook configuration (`group_vars/servers` or other):

```yaml
# See `devture_systemd_service_manager_services_list_auto` and `devture_systemd_service_manager_services_list_additional`
devture_systemd_service_manager_services_list_auto: |
  {{
    ([{'name': 'some-service.service', 'priority': 1000}])
    +
    ([{'name': 'another-service.service', 'priority': 1500}])
  }}
```

Example playbook invocations:

- `ansible-playbook -i inventory/hosts setup.yml --tags=start` (restarts all services and potentially makes them auto-start)

- `ansible-playbook -i inventory/hosts setup.yml --tags=stop` (stops all services)
