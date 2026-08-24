ABOUT
=====

A radically simple Ansible Role.
- System: Debian 13

PLAYBOOK
========

```yml
- ansible.builtin.import_role:
    name: systemd-units
  vars:
		systemd_units:
		- name: app-worker
			type: service
			state: started
			enabled: true
			config:
				Unit:
					Description: Custom App Worker Process
					After: network.target
				Service:
					Type: simple
					User: appuser
					ExecStartPre:
          - "/usr/local/bin/check-db.sh"
          - "/usr/local/bin/prep-env.sh"
					ExecStart: "/usr/local/bin/app-worker --port 8080"
					Restart: on-failure
					RestartSec: 5
				Install:
					WantedBy: multi-user.target
```
