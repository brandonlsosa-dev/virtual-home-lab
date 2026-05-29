# Network design

## Subnet table

| Subnet     | Network           | CIDR             | Purpose                   |
|------------|-------------------|------------------|---------------------------|
| WAN        | VMware NAT/VMnet8 | 192.168.0.0/24   | pfSense internet uplink   |
| Server LAN | VMnet2 host-only  | 192.168.10.0/24  | Domain controller + Ubuntu|
| Client LAN | VMnet3 host-only  | 192.168.20.0/24  | Windows 10 workstation    |
| Management | VMnet4 host-only  | 192.168.30.0/24  | Admin SSH / RDP access    |

## Design decisions

- pfSense used as virtual firewall and router between all subnets
- VMware DHCP disabled on VMnet2 and VMnet3 — Windows Server 
  acts as DHCP server for those subnets to mirror enterprise design
- VMnet4 keeps VMware DHCP enabled for host machine management access
- /24 subnets chosen for simplicity and alignment with 
  small-to-medium business conventions

## VMnet configuration

| VMnet  | Type      | Subnet          | DHCP              |
|--------|-----------|-----------------|-------------------|
| VMnet2 | Host-only | 192.168.10.0/24 | Disabled          |
| VMnet3 | Host-only | 192.168.20.0/24 | Disabled          |
| VMnet4 | Host-only | 192.168.30.0/24 | Enabled (VMware)  |
| VMnet8 | NAT       | assigned by VMware | Enabled (VMware)|
