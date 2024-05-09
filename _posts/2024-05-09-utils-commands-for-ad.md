---
layout: post
title:  "Utils commands for Active Directy and LDAP"
date:   2023-12-05 12:00:00 -0300
categories: tutorial linux ad
---

## Commands for Windows Server

```bash
# Add/remove Domain Controllers
dcpromo

# Get list of all Domain Controllers
nltest /dclist:mylab.lan

# Query for DC with FSMO
netdom query fsmo

# Show info about DC
nltest /dsgetdc:mylab.lan

# Get replicated data and send to clipboard
repadmin /showrepl | clip

# Replicate data between DCs
repadmin /replicate server01 server02 <DATA> /force

# Register new dll on windows
regsvr32 schmmgmt.dll

# Microsoft Management Console
mmc
```

## Commands for Zentyal

```bash
# Show info about DC
samba-tool domain info 127.0.0.1

# Check database and fix erros
samba-tool dbcheck --cross-ncs --yes --fix -v
samba-tool dbcheck --cross-ncs --yes

# List all users
samba-tool user list

# Query for DC with FSMO
samba-tool fsmo show
```

## References

[Youtube Channel SysAdminBr](https://youtube.com/playlist?list=PLFajyb7NamFDqLmrUIddr_euDkRcWMgQ9&si=ka7L_knXEGDax5ip)
