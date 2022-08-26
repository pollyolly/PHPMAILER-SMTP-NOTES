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
```
Check SMTP port
```
$nmap -p<port> <smtp-host-ip>
```
