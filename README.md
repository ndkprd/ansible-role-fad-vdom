ndkprd.fad_vdom
===============

An Ansible role to manage Fortinet's FortiADC VDOMs via HTTP REST API.

Requirements
------------

FortiADC:
- a REST API user with enough permission.

Role Variables
--------------

| Variable Name       | Type          | Default Value | Description     |
|---------------------|---------------|---------------|-----------------|
| fad_vdoms           | list of dicts | []            | List of VDOMs.  |
| fad_vdoms[x].name   | str           | -             | VDOM name/mkey. |
| fad_vdoms[x].status | str           | enabled       | VDOM status.    |


Dependencies
------------

At this point in time this role don't have any dependencies to any other roles.

Examples
----------------

Inventory:

```ini
[fortiadc]
fad-01 ansible_host=fad-01.infra.ndkprd.com ansible_connection=local fad_apitoken=mysupersecrettoken fad_vdom=root

[fortiadc:vars]
http_port=80
https_port=443
```

Playbook:

```yaml
---

- name: Update/create FortiADC resources.
  hosts: all
  become: false
  gather_facts: false
  connection: local
  vars:
    fad_vdoms:
    - name: development
      status: enable
    - name: staging
      status: enable
    - name: production
      status: enable

  roles:
    - ndkprd.fad_vdom
```

License
-------

MIT
