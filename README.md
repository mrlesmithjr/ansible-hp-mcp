<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [ansible-hp-mcp](#ansible-hp-mcp)
  - [Functionality](#functionality)
  - [Requirements](#requirements)
  - [Role Variables](#role-variables)
  - [Dependencies](#dependencies)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# ansible-hp-mcp

An [Ansible](https://www.ansible.com) role to install [HP Management Component Pack](https://downloads.linux.hpe.com/SDR/project/mcp/)

## Functionality

-   Configure ILO
    -   users
    -   networking
    -   licensing

## Requirements

Requires HP Proliant Server

## Role Variables

```yaml
---
# defaults file for ansible-hp-mcp
hp_mcp_config_ilo: false

hp_mcp_debian_repo_info:
  keys:
    - 'http://downloads.linux.hpe.com/SDR/hpPublicKey1024.pub'
    - 'http://downloads.linux.hpe.com/SDR/hpPublicKey2048.pub'
    - 'http://downloads.linux.hpe.com/SDR/hpPublicKey2048_key1.pub'
    - 'http://downloads.linux.hpe.com/SDR/hpePublicKey2048_key1.pub'
  repo: 'deb http://downloads.linux.hpe.com/SDR/repo/mcp {{ ansible_distribution_release|lower }}/current non-free'

# http://h20564.www2.hpe.com/hpsc/doc/public/display?docId=c03334058
hp_mcp_ilo_config:
  enable_dhcp: true
  enable_ssh: false
  serial_cli_speed: 5
  serial_cli_status: 3
  session_timeout: 15
  ssh_port: 22

hp_mcp_ilo_config_dir: '/root'

hp_mcp_ilo_default_admin_password: 'password'

hp_mcp_ilo_dns_name: "{{ hostvars[inventory_hostname]['inventory_hostname_short'] }}-ilo"

hp_mcp_ilo_domain_name: 'vagrant.local'

hp_mcp_ilo_gateway: 192.168.1.1

hp_mcp_ilo_ip: 192.168.1.125

hp_mcp_ilo_license: []

hp_mcp_ilo_prim_dns: 192.168.1.10

hp_mcp_ilo_sec_dns: 192.168.1.11

hp_mcp_ilo_subnet_mask: 255.255.255.0

hp_mcp_ilo_users: []
  # - user_name: 'admin1'
  #   admin_priv: true
  #   config_ilo_priv: true
  #   password: 'password'
  #   remote_cons_priv: true
  #   reset_server_priv: false
  #   state: 'present'
  #   virtual_media_priv: true
  # - user_name: 'admin2'
  #   admin_priv: true
  #   config_ilo_priv: true
  #   password: 'password'
  #   remote_cons_priv: true
  #   reset_server_priv: false
  #   state: 'absent'
  #   virtual_media_priv: true

hp_mcp_storage_controllers: []
  # - slot: 0
  #   arrays:
  #     - array: 'A'
  #       physicaldisks:
  #         - '1I:1:1'
  #         - '1I:1:2'
  #       raid: 1
  #     - array: 'B'
  #       physicaldisks:
  #         - '1I:1:3'
  #         - '1I:1:4'
  #         - '1I:1:5'
  #         - '1I:1:6'
  #       raid: 5

hp_mcp_tools:
  # HPE System Health Application and Command line Utilities
  - 'hp-health'
  # HPE RILOE II/iLO online configuration utility
  - 'hponcfg'
  # HPE Agentless Management Service (Requires ILO 4)
  # - 'hp-ams'
  # Insight Management SNMP Agents for HPE ProLiant Systems
  - 'hp-snmp-agents'
  # HPE System Management Homepage
  # - 'hpsmh'
  # HPE System Management Homepage Templates
  # - 'hp-smh-templates'
  # HPE Command Line Smart Storage Administration Utility
  - 'hpssacli'
  # HPE Command Line Smart Storage Administration Diagnostics
  # - 'hpssaducli'
  # HPE Array Smart Storage Administration Service
  - 'hpssa'
```

## Dependencies

## Example Playbook

```yaml
---
- hosts: all
  roles:
    - role: ansible-hp-mcp
      when: >
            ansible_system_vendor == "HP" and
            ('ProLiant' in ansible_product_name)
```

## License

MIT

## Author Information

Larry Smith Jr.

-   [@mrlesmithjr](https://www.twitter.com/mrlesmithjr)
-   [EverythingShouldBeVirtual](http://everythingshouldbevirtual.com)
-   [mrlesmithjr.com](http://mrlesmithjr.com)
-   mrlesmithjr [at] gmail.com
