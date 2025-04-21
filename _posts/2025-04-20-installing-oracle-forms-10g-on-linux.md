---
layout: post
title: "Installing Oracle Forms 10g on Linux with WineHQ"
date: 2025-04-20 19:00:00 -0300
categories: tutorial linux wine
---
Welcome to the tutorial of how to install Oracle Forms and Reports 10g on Ubuntu 24.04 LTS distribution.

The next steps will install WineHQ, you can check this informations on [Wine Official Wiki](https://gitlab.winehq.org/wine/wine/-/wikis/Debian-Ubuntu).

```bash
# Delete .wine folder
# THIS WILL DELETE ALL WINE APPS!
rm -rf ~/.wine
rm -rf ~/.local/share/applications/wine

# Remove all others wine version
sudo apt remove --purge wine* fonts-wine
sudo apt autoremove

# Delete .cache folder and reboot

# Enable 32 bit architecture
sudo dpkg --add-architecture i386

# Add the public key
# Make sure the directory exist
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key

# Add the source file for 24.04 (noble)
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources

# Install WineHQ and Mono
sudo apt update
sudo apt install --install-recommends winehq-stable
sudo apt install --install-recommends mono-complete

# Start a Wine 32bit Prefix
# A Wine Mono window will prompted. Click on button Install
WINEPREFIX=~/wine10g WINEARCH=win32 wineboot -u

# Open IExplorer. A Wine Gecko window will prompted. Click on button Install
WINEPREFIX=~/wine10g wine iexplore

# IMPORTANT: You need to change version to Windows XP
WINEPREFIX=~/wine10g winecfg

# Copy file MemoryManagement.reg to ~/.wine/drive_c/
# Import reg file with regedit
cd ~/.wine/drive_c/
WINEPREFIX=~/wine10g wine regedit

# Copy installer folder Oracle_Developer_Suite_10g with Disk1 and Disk2 to ~/.wine/drive_c/
cd ~/.wine/drive_c/Oracle_Developer_Suite_10g/Disk1/
WINEPREFIX=~/wine10g wine setup.exe

# Follow: Next > Next > Next > (*) Complete > Next > Next > Install > Exit > Yes
# Reboot your system

# Run Oracle Database 11g with Docker
# Create a folder with file `compose.yml`
docker compose up -d

# On launcher, start application Net Manager
# Go to Local > Service Name > Plus button
# Name: XE > Next > TCP/IP > Next > Host: localhost > Next >
# Service name: XE > Next > Finish > Save

# On launcher, start SQLPlus
# Username: system
# Password: oracle
# String: xe
# Create some users anf table for teste
```

You need to install Winetricks using Github script provided by [README.md Winetrick Repository](https://github.com/Winetricks/winetricks). After run the script you can do:

```
# Update Winetrick to last version
update_winetricks

# Install IE7
WINEPREFIX=~/wine10g winetricks ie7

# Add iertutil in library tab on Wine Configuration
WINEPREFIX=~/wine10g winecfg

# On launcher, start OC4J Instance
# On launcher, start Forms Builder
# Connect to database on Forms
# Create or open some project and Run

# Download and install the JInit
# http://localhost:8889/forms/jinitiator/jinit.exe
WINEPREFIX=~/wine10g wine jinit.exe

# Copy URL opened, and run on IE7
WINEPREFIX=~/wine10g wine 'C:\Program Files\Internet Explorer\iexplore.exe'

# Replace jvm.dll for a JDK 1.5 version
# .wine/drive_c/Program Files (x86)/Oracle/JInitiator 1.3.1.22/bin/hotspot/
```

### Content of file `MemoryManagement.reg`

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management]
"ClearPageFileAtShutdown"=dword:00000000
"DisablePagingExecutive"=dword:00000000
"LargeSystemCache"=dword:00000000
"NonPagedPoolQuota"=dword:00000000
"NonPagedPoolSize"=dword:00000000
"PagedPoolQuota"=dword:00000000
"PagedPoolSize"=dword:00000000
"SecondLevelDataCache"=dword:00000000
"SessionPoolSize"=dword:00000004
"SessionViewSize"=dword:00000030
"SystemPages"=dword:00000000
"PagingFiles"=hex(7):63,00,3a,00,5c,00,70,00,61,00,67,00,65,00,66,00,69,00,6c,\
  00,65,00,2e,00,73,00,79,00,73,00,20,00,31,00,35,00,33,00,35,00,20,00,31,00,\
  35,00,33,00,35,00,00,00,00,00
"PhysicalAddressExtension"=dword:00000001
"ExistingPageFiles"=hex(7):5c,00,3f,00,3f,00,5c,00,43,00,3a,00,5c,00,70,00,61,\
  00,67,00,65,00,66,00,69,00,6c,00,65,00,2e,00,73,00,79,00,73,00,00,00,00,00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PrefetchParameters]
"BootId"=dword:00000023
"BaseTime"=dword:2ca33473
"EnableSuperfetch"=dword:00000003
"EnablePrefetcher"=dword:00000003
"EnableBootTrace"=dword:00000000

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\StoreParameters]
```

### Content of file `compose.yml`

```
services: 
  oracle-db:
    image: oracleinanutshell/oracle-xe-11g:latest
    environment:
      - ORACLE_DISABLE_ASYNCH_IO=true
      - ORACLE_ALLOW_REMOTE=true
      - ORACLE_ENABLE_XDB=true
    ports:
      - 1521:1521
      - 5500:5500
      - 49161:1521
      - 8080:8080

# username: system
# password: oracle
# sid: xe
# hostname: localhost
# DOCUMENTATION: https://hub.docker.com/r/oracleinanutshell/oracle-xe-11g
```

### Samples of SQL commands for SQLPlus

```sql
CREATE USER nota_fiscal IDENTIFIED BY 123;
ALTER USER nota_fiscal quota unlimited on USERS;
ALTER USER nota_fiscal quota unlimited on SYSTEM;
GRANT CREATE SESSION TO nota_fiscal;

CREATE TABLE NOTA_FISCAL.CLIENTES (
	"CODIGO" NUMBER(38,0) NOT NULL ENABLE, 
	"NOME" VARCHAR2(100), 
	 CONSTRAINT "CLIENTE_PK" PRIMARY KEY ("CODIGO")
);

CREATE TABLE NOTA_FISCAL.PRODUTOS (
	"CODIGO" NUMBER(38,0) NOT NULL ENABLE, 
	"NOME" VARCHAR2(100) NOT NULL ENABLE,
	"PRECO_UNITARIO" NUMBER(16,2),
	 CONSTRAINT "PRODUTOS_PK" PRIMARY KEY ("CODIGO")
);

CREATE TABLE NOTA_FISCAL.VENDAS (
	"CODIGO" NUMBER(38,0) NOT NULL ENABLE, 
	"DATA" DATE NOT NULL ENABLE, 
	"CLIENTE_ID" NUMBER(38,0) NOT NULL ENABLE,  
	"OBSERVACAO" VARCHAR2(100), 
	 CONSTRAINT "VENDAS_PK" PRIMARY KEY ("CODIGO")
);

ALTER TABLE
	NOTA_FISCAL.VENDAS
	ADD CONSTRAINT "VENDAS_CLIENTE_FK"
	FOREIGN KEY ("CLIENTE_ID")
	REFERENCES "NOTA_FISCAL"."CLIENTES" ("CODIGO") ENABLE;

CREATE TABLE NOTA_FISCAL.VENDAS_ITENS (
	"VENDAS_ID" NUMBER(38,0), 
	"QUANTIDADE" NUMBER(38,0), 
	"PRODUTO_ID" NUMBER(38,0),
	"UF" VARCHAR(2)
);
```
