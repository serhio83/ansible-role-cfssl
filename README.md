# ansible-role-cfssl

Installes CFSSL (CloudFlare's PKI toolkit) binaries.

inventory example:

```
all:
  children:
    consul_servers:
      hosts:
        s01.dev.lab: {}
        s02.dev.lab: {}
        s03.dev.lab: {}
      vars:
        consul_role: "server"
    ks:
      hosts:
        s04.dev.lab: {}
      vars:
        consul_role: "client"
    monitoring:
      children:
        consul_agents:
          hosts:
            s05.dev.lab: {}
          vars:
            consul_role: "client"
```

playbook example:

```
- name: Gather facts once on start
  hosts: all
  gather_facts: true
  tags:
    - always

- name: Prepare keystore
  hosts: ks
  gather_facts: false
  roles:
    - cfssl
```
