Role Name
=========

ESXi_dns configure dns parameters in our ESXi servers

Requirements
------------

No requirements

Role Variables
--------------

Is necessary that variables `dns1`, `dns2` & `domain` has been defined in our inventory file

Example:

```ini
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
```

Dependencies
------------

No dependencies

Example Playbook
----------------

This play is executed when update_mode var is "true" and ensure that role is up to date. By default update var is "false"

miquelMariano.ESXi_{{ role }} folder must be exist. If not, the playbook not found role and fails. You shoud make dir manually "mkdir /etc/ansible/my_role"

```yaml
###
###ESXi_config.yml
###		
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
  serial: 1
  roles:
   - role: miquelMariano.ESXi_{{ role  }}
~
~
~

```

Usage
------

```ssh
ansible-playbook playbooks/ESXi_config.yml -i inventory/ESXi --extra-vars "servers=esxi role=dns update_mode=true" --tags "update,set"
```


License
-------

BSD

Author Information
------------------

[miquelMariano.github.io](https://miquelMariano.github.io) | [Twitter](https://twitter.com/miquelMariano)

