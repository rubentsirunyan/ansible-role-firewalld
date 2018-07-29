Ansible Role: Firewalld
=======================

This role is a simple wrapper over Ansible's `firewalld` module to bulk configure firewalld zones.

Requirements
------------

None

Role Variables
--------------

`firewalld_apply_immediately` Set this to `true` to apply all the rules immediately. Default `true`

`firewalld_apply_permanently` Set this to `true` for the rules to persist across reboots. Default `false`

Zone configurations with the default values. Self explanatory.

    firewalld_zones:
      - zone: internal
        interface: "{{ ansible_default_ipv4.interface }}"
        services: []
        ports: []
        sources: []

Dependencies
------------

None.

Example Playbooks
----------------

#### Example: Single zone

    - hosts: web_servers
      tasks:
        - include_role: 
            name: rubentsirunyan.firewalld 
          vars:
            firewalld_apply_immediately: true
            firewalld_apply_permanently: true
            firewalld_zones:
              - zone: internal
                interface: eth0
                services:
                  - http
                  - https
                ports:
                  - 8080
                sources:
                  - 192.168.0.0/24

#### Example: Multiple zone

    - hosts: servers
      tasks:
        - include_role: 
            name: rubentsirunyan.firewalld 
          vars:
            firewalld_apply_immediately: true
            firewalld_apply_permanently: true
            firewalld_zones:
              - zone: internal
                interface: eth0
                services:
                  - dns
                  - dhcp
                sources:
                  - 192.168.0.0/24
              - zone: public 
                interface: eth1
                ports:
                  - 10454

License
-------

GNU General Public License v3.0

Author Information
------------------

This role was created by [Ruben Tsirunyan](https://github.com/rubentsirunyan)
