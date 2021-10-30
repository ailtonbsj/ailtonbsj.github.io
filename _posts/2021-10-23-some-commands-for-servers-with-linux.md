---
layout: post
title: "Some commands for servers with linux"
date: 2021-10-23 20:00:00 -0300
categories: tutorial linux server
---
This is a list of some utils commands for servers linux:

## NTP Commands

```bash
# Install ntp deamon and tools
apt install ntp ntpdate

# Edit file /etc/ntp.conf to change server to brazil
## server a.st1.ntp.br iburst
## server b.st1.ntp.br iburst
## server c.st1.ntp.br iburst
## server d.st1.ntp.br iburst
## server a.ntp.br iburst
## server b.ntp.br iburst
## server c.ntp.br iburst
## disable monitor

# Restart deamon
systemctl restart ntp.service

# Query a list of ntp servers used
ntpq -p

# Query the current date and time from ntp server
ntpdate -q 192.168.1.1
```

## Kerberos Commands

```bash
# Install kerberos
apt install krb5-user krb5-config
# Set default realm: EMPRESA.INTRA
# Set hostname server: serverdc01.empresa.intra
# Set admin server: serverdc01.empresa.intra

# Recomends do backup of conf file
cp /etc/krb5.conf /etc/krb5.conf.bkp
```

## RAID with LVM

```bash
# List infos about disks
lshw -class disk

# List infos about partitions
fdisk -l

# List partitions by disk
cfdisk -Ps /dev/sda

# List UUID of disks
blkid

# Create partitions and format as RAID auto
fdisk /dev/sdc
## Subterminal commands (use m for help):
## n p 1 [Enter] [Enter] p t L fd p w

# Create device /dev/md1 RAID type 1
mdadm -C -v /dev/md1 -l 1 -n 2 /dev/sdc1 /dev/sdd1

# See status of raid devices
cat /proc/mdstat

# See detail do raid device
mdadm -D /dev/md1

# Format partition as ext4
mkfs.ext4 /dev/md1

# See detail do raid partition
mdadm -E /dev/sdc1

# List all md device and infos
mdadm -D --scan

# Append mdadm.conf with infos of md device
mdadm -D --scan | grep m1 >> /etc/mdadm/mdadm.conf

# Generate initramfs image with md devices
update-initramfs -u

# Mount and umount raid partition
mount /dev/md1 /arquivos
umount /arquivos

# List infos mounted device
mount -l | grep /arquivos

# Append UUID from RAID on fstab file
blkid /dev/md1 | cut -d' ' -f2 >> /etc/fstab
```

## Access control list and Extended attributes

```bash
# Install packages
apt install acl attr

# Get name, owner, group, permissions and ACL
getfacl file.txt

# Set ACL on file for user and group
setfacl -m user:jose.ailton:rwx -d file.txt
setfacl -m group:"EMPRESA\Domain Admins":rwx -d file.txt

# Get all extended attributes
getfattr file.txt

# Get an extended attribute
getfattr -n user.author file.txt

# Set extended attribute for an user
setfattr -n user.author -v "Jose Ailton" file.txt

# Change default group of file
chgrp "EMPRESA\Domain Admins" file.txt
```

## Network commands

```bash
# Show infos about PCI devices
lspci

# Show infos about network devices
lshw -class network
mii-tool enp0s3
ethtool enp0s3

# Show network interfaces (ip, mask and broadcast)
ifconfig

# Show IP route table (gateway)
route -n

# Show DNS servers (dns)
cat /etc/resolv.conf

# Enable/disable network adapter
ifup enp0s3
ifdown enp0s3

vim /etc/dhcp3/dhclient.con
# Uncomment to configure dns servers over dhcp sets:
## prepend domain-name-servers 127.0.0.1;

vim /etc/network/interfaces
## auto eth0
## iface eth0 inet dhcp
##
## auto eth1
## iface eth1 inet static
## address 192.168.2.1
## netmask 255.255.255.0
## network 192.168.2.0
## broadcast 192.168.2.255
## gateway 192.168.2.1 <-- don't use if there's another
## dns-nameservers 192.168.2.1 1.1.1.1
## dns-search empresa.intra
## dns-domain empresa.intra

# Flush the interface if error
ip addr flush dev enp0s8

# Restart network daemon
systemctl restart networking.service

vim /etc/hosts
# Append line:
## 192.168.2.1 serverdc01.empresa.intra serverdc01
```

## Samba and AD

```bash
# Install samba
apt install samba smbclient cifs-utils samba-vfs-modules samba-testsuite samba-dbg samba-dsdb-modules cups

# Show samba version
smbd -V

# Stop samba deamon
systemctl stop smbd.service

# Provisioning samba as AD
samba-tool domain provision --use-rfc2307 --use-xattrs=yes --use-ntvfs --interactive
## Realm: empresa.intra
## Domain: empresa
## Server Role: dc
## DNS backend: SAMBA_INTERNAL
## DNS forwarder: 10.0.2.3
## Admin pass: [Strong password]
## Then copy kerberos conf file:
cp /var/lib/samba/private/krb5.conf /etc/

# Check level of AD
samba-tool domain level show

# Raise level of AD
samba-tool domain level raise --domain-level 2008_R2 --forest-level 2008_R2

# Show all port used by samba
netstat -teulpen | grep /samba

# Show all process of samba
ps -auxf | grep -i samba

# Show priorities of Name service
cat /etc/nsswitch.conf

# Show and check parameters of samba
samba-tool testparm

# Show infos of domain
samba-tool domain info 192.168.2.1
samba-tool domain info empresa.intra

# Check erros in database samba
samba-tool dbcheck

# Show current datetime
samba-tool time

# List all gpo in AD
samba-tool gpo listall

# List all groups in AD
samba-tool group list

# List all users in AD
samba-tool group list

# Show infos about passwords 
samba-tool domain passwordsettings show

# DNS Query on AD Samba
samba-tool dns query serverdc01 EMPRESA.INTRA @ ALL --username administrator

# List samba folders
smbclient -L localhost -U%
smbclient -L empresa.intra -U%

# List files of an samba folder
smbclient //empresa.intra/netlogon -U 'administrator'
## use subterminal:
## ls

# Query IP in a DNS Server
host -t A serverdc01.empresa.intra
nslookup serverdc01.empresa.intra
host -t SRV _ldap._tcp.empresa.intra
host -t SRV _kerberos._udp.empresa.intra

# Check about Kerberos ticket auth
kinit administrator@EMPRESA.INTRA

# Check cache ticket kerberos
klist

# Create new user on domain
samba-tool user add joao.batista

# Create new user on domain inside OU
samba-tool user add joao.batista --userou=OU=Users,OU=Sales,OU=empresa.intra

# Create new group on domain
samba-tool group add Sales --description "Just a group"

# Create new group on domain inside OU
samba-tool group add Sales --group-scope=Global --groupou=OU=Groups,OU=Sales,OU=empresa.intra
samba-tool group add FolderSales --group-scope=Domain --groupou=OU=Groups,OU=Sales,OU=empresa.intra

# Add member to a group
samba-tool addmembers Sales joao.batista

# List all members of a group
samba-tool listmembers Sales

# Show canonical name of user or group
samba-tool spn list joao.batista

vim /etc/smb.conf
# Append in global session:
## vfs objects = acl_xattr
## map acl inherit = yes
## store dos attributes = yes
# Append on end of file:
## [Publico]
##    path = /arquivos/Publico
##    read only = No

# Test if smb.conf is OK
testparm
```

## DHCP Server
```bash
# Install DHCP Server
apt install isc-dhcp-server

# Check status of daemon
systemctl status isc-dhcp-server.service

# Do backup con dhcp conf file
cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bkp

# Set interface of dhcp server
vim /etc/default/isc-dhcp-server
# INTERFACES="enp0s8"

# Edit dhcp file conf
vim /etc/dhcp/dhcpd.conf
## ddns-update-style interim;
## ddns-updates on;
## option domain-name "empresa.intra";
## option domain-name-servers 192.168.2.1;
## option ntp-servers 192.168.2.1;
## authoritative;
## subnet 192.168.2.0 netmask 255.255.255.0 {
##  range 192.168.2.100 192.168.2.200;
##  option domain-name-servers 192.168.2.1 1.1.1.1;
##  option domain-name "empresa.intra";
##  option netbios-name-servers 192.168.2.1;
##  option netbios-dd-server 192.168.2.1;
##  option netbios-node-type 8;
##  option routers 192.168.2.1;
##  option broadcast-address 192.168.2.255;
##  option subnet-mask 255.255.255.0;
##  option ntp-servers 192.168.2.1;
##  default-lease-time 600;
##  max-lease-time 7200;
##  allow unknown-clients;
## }

# Check if dhcp conf file has errors
dhcpd -cf /etc/dhcp/dhcpd.conf

# Show all borrowed ip's
cat /var/lib/dhcp/dchpd.leases
```

## IP Forward, NAT and Masquerading

```bash
# Enable Global Routing on the fly
echo 1 > /proc/sys/net/ipv4/ip_forward

# Enable Global Routing permanently
# Set option: net.ipv4.ip_forward = 1
vim /etc/sysctl.conf
sysctl -p /etc/sysctl.conf

# Accept forwarding all packages coming from enp0s8
iptables -A FORWARD -i enp0s8 -j ACCEPT

# Accept forwarding all packages to enp0s8
iptables -A FORWARD -o enp0s8 -j ACCEPT

# Masquerade all packages that are sent to enp0s3
iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE

# Save current rules of iptable on file
iptables-save | sudo tee /etc/iptables.conf

# Load rules on iptables on init
vim /etc/rc.local
## Add before exit 0:
## iptables-restore < /etc/iptables.conf
```

## IPTables commands

```bash
# See rules of Firewall
iptables -nL
iptables -t nat -nL

# Clean all rules of table
iptables -F
iptables -t nat -F

# Change policy of chain input as drop
iptables -P INPUT DROP

# Accept input of icmp packages (ping) from anywhere by enp0s8 to destination 192.168.2.1
iptables -A INPUT -s 0/0 -i enp0s8 -d 192.168.2.1 -p ICMP -j ACCEPT

# Drops input of icmp packages type 8 with destination 192.168.1.{1-254}
iptables -A INPUT -p icmp --icmp-type 8 -d 192.168.1.0/24 -j DROP
```

## CID Client AD

```bash
# Show infos about domain
cid status
```

## WINBIND

```bash
# Install WINBIND
apt install winbind quota quotatool ldb-tools libnss-winbind libpam-winbind

vim /etc/nsswitch.conf
# Edit lines:
## passwd: compat winbind
## group: compat winbind
## shadow: compat winbind

# Edit sam database
ldbedit -H /var/lib/samba/private/sam.ldb -e vim -b CN=empresa,CN=ypservers,CN=ypServ30,CN=RpcServices,CN=System,DC=empresa,DC=intra
## Append:
## msSFU30MaxUidNumber: 10000
## msSFU30MaxGidNumber: 20000

# Apply confs on samba
smbcontrol all reload-config

#
net rpc rights list accounts -UAdministrator

#
net rpc rights grant 'EMPRESA\Domain Admins' SeDiskOperatorPrivilege -UAdministrator

# Ping on winbind
wbinfo -p

# List winbind users, groups
 wbinfo -u
 wbinfo -g

# Get entries from Name Service Switch
getent passwd "administrator"
getent group "G-Financeiro"

# Display details on remote ADS server
net ads info
```
