Role Name
=========

ESXi_dns configure dns parameters in our ESXi servers

Requirements
------------

No requirements

Role Variables
--------------

Is necessary that variables ntp1 & ntp2 has been defined in our inventory file

Example:

		[all]
		servers_group1
		servers_group2

		[servers_group1]
		server1
		server2
		server3

		[servers_group2]
		server11
		server12
		server13

		[all:vars]
		dns1='172.25.34.100'
		dns2='172.25.34.101'
		domain='corp.ncora.com'

Dependencies
------------

No dependencies

Example Playbook
----------------

This play is executed when update_mode var is "true" and ensure that role is up to date. By default update var is "false"

miquelMariano.ESXi_{{ role }} folder must be exist. If not, the playbook not found role and fails. You shoud make dir manually "mkdir /etc/ansible/my_role"

```
		- hosts: ansible
 		  user: root
 		  tasks:
 		   - name: Ensure that role are up to date
 		     command: ansible-galaxy install --force {{ item }}
 		     with_items:
 		       - miquelMariano.ESXi_{{ role  }}
 		     when:
 		       - update_mode | default(False)
 		     tags: update
 		     ignore_errors: yes

		- hosts: "{{ servers }}:!localhost"
		  user: root
 		  serial: 15
 		  roles:
 		  - role: miquelMariano.ESXi_{{ role }}
```

Usage
------

`ansible-playbook playbooks/ESXi_config.yml -i inventory/ESXi --extra-vars "servers=servers_group1 role=dns update_mode=true" --tags "update|set"`


License
-------

BSD

Author Information
------------------

[@miquelMariano](https://twitter.com/miquelMariano)

