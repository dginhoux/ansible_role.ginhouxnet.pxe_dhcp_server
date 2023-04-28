# ROLE dginhoux.pxe_dhcp_server



## DESCRIPTION

This ansible role configure isc-dhcp-server.<br />
NOTE : Only ipv4 is configured, not enough ipv6 knowledges.


## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip process with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `skip_check_platform_compatibility=True`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36, 37, 38 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.pxe_dhcp_server
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.pxe_dhcp_server dginhoux.pxe_dhcp_server
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.pxe_dhcp_server
      ansible.builtin.include_role:
        name: dginhoux.pxe_dhcp_server
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
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
    tftp: pxe.infra.ginhoux.net
    domain: ginhoux.net
    allow_booting: "true"
    allow_unknown_clients: "false"
    max_lease_time: 84600
    default_lease_time: 3600

dhcp_leases4:
  - network: 192.168.175.0
    boot_bios_filename: syslinux/bios/pxelinux.0
    boot_bios_pathprefix: syslinux/bios/
    boot_efi64_filename: syslinux/efi64/syslinux.efi
    boot_efi64_pathprefix: syslinux/efi64/
    leases:
      - name: srv-swarm-manager1.infra.ginhoux.net
        ipaddr: 192.168.175.101
        macaddr: DC:10:00:17:51:01
      - name: srv-swarm-manager2.infra.ginhoux.net
        ipaddr: 192.168.175.102
        macaddr: DC:10:00:17:51:02
        boot_bios_filename: syslinux/bios_specific/pxelinux.0
        boot_bios_pathprefix: syslinux/bios_specific/
        boot_efi64_filename: syslinux/efi64_specific/syslinux.efi
        boot_efi64_pathprefix: syslinux/efi64_specific/
      - name: srv-swarm-manager3.infra.ginhoux.net
        ipaddr: 192.168.175.103
        macaddr: DC:10:00:17:51:03
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.


* Debian family : 

```yaml
dhcp_service: isc-dhcp-server

dhcp_debian_default_file: /etc/default/isc-dhcp-server
```

* RedHat family : 

```yaml
dhcp_service: dhcpd
```



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
