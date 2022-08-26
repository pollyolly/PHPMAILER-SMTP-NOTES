### SMTP-Notes
Check connection
```
$telnet <smtp-host-ip> 25
```
Install nmap to check ports and connections
```
$apt-get install nmap
```
Check SMTP available ports
```
$nmap <smtp-host-ip>

Nmap scan report for 10.16.11.129
Host is up (0.0047s latency).
Not shown: 995 filtered ports
PORT     STATE SERVICE
22/tcp   open  ssh
25/tcp   open  smtp
110/tcp  open  pop3
587/tcp  open  submission
1720/tcp open  h323q931
```
Check SMTP port
```
$nmap -p<port> <smtp-host-ip>
```
