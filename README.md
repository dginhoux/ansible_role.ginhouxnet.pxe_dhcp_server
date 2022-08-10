ginhouxnet.pxe_dhcp_server
=========

This ansible role configure isc-dhcp-server.
Only ipv4 is configured, not enough ipv6 knowledges.


Requirements
------------

This ansible role will only run on identified OS defined on meta/main.yml


Role Variables
--------------


```
dhcp_configure_action: generate
# dhcp_configure_action: cleanup

dhcp_main_config4_file: /etc/dhcp/dhcpd.conf
dhcp_main_config6_file: /etc/dhcp/dhcpd6.conf
dhcp_config_dir: /etc/dhcp
dhcp_sub_config_dir: /etc/dhcp/dhcpd.d

dhcp_subnets4:
  - network: 192.168.175.0
    netmask: 255.255.255.0
    range: 192.168.175.1 192.168.175.9
    gateway: 192.168.175.254
    dns: 192.168.175.10
    ntp: 192.168.175.10
    tftp: 192.168.175.180
    domain: infra.ginhoux.net

dhcp_leases4:
  - network: 192.168.175.0
    leases:
      - name: test.infra.ginhoux.net
        ipaddr: 192.168.175.1
        macaddr: AA:BB:CC:00:11:22

dhcp_subnets6: []

dhcp_leases6: []

```


Dependencies
------------




Example Playbook
----------------



License
-------

BSD


Author Information
------------------

Dany GINHOUX
