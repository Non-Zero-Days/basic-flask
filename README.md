# Python Flask

## Prerequisites:
- Install [Python](https://www.python.org/downloads/)
- Install [Postman](https://www.postman.com/downloads/)

## Loose Agenda:
- Gain basic familiarity with Flask
- Get exposure to HTTP concepts

## Step by Step

### Setup Playground
Create a directory for this exercise

Open Visual Studio Code

Select File > Open Folder and select the directory that was created in the first step

On the left side nav menu select the topmost icon to open the Explorer window (Alternatively, use the hot-key Ctrl+Shift+E)

Right click in the Explorer window, select "New File" then enter the name app.py


### Install Flask

Run the following command

```
pip install flask
```

### Create a GET endpoint in app.py

Populate your app.py file with the following code

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def basic_endpoint():
    return 'Happy Non-Zero Day!'

app.run()
```

### Call our endpoint

Run your application with the following command in a terminal

```
py app.py
```

Open Postman

Create a new request

Select GET

Enter the request URL

```
localhost:5000
```

Send request

Review results

### Adjust your endpoint's route

Change the app.py code to 

```
app = Flask(__name__)

@app.route('/motd')
def basic_endpoint():
    return 'Happy Non-Zero Day!'
```

Run the application again

```
py app.py
```

Update route in Postman to

```
localhost:5000/motd
```

Send request

Review results

### Return a value from a file

Create a new file called motd.txt and populate it with:

```
Happy Non-Zero Day!
```

Adjust app.py to return the contents of the file

```
from flask import Flask
app = Flask(__name__)

@app.route("/motd")
def messageoftheday():
    with open("motd.txt", 'r') as file:
        return file.read()

app.run()

```

Run the application again

```
py app.py
```

Set route in Postman to

```
localhost:5000/motd
```

Send request

Review results

**Note that you can change the contents of the motd.txt while the application is running and the results will change**


### Create a POST endpoint in app.py

Add an import for request from the flask library
```
from flask import Flask
from flask import request
app = Flask(__name__)

@app.route("/motd")
def messageoftheday():
    with open("motd.txt", 'r') as file:
        return file.read()

app.run()

```

Adjust app.py to include a POST endpoint which modifies the motd.txt

```
from flask import Flask
from flask import request
app = Flask(__name__)

@app.route("/motd")
def messageoftheday():
    with open("motd.txt", 'r') as file:
        return file.read()

@app.route("/setmotd", methods=['POST'])
def setmessageoftheday():
    with open("motd.txt", 'w') as file:
        data = request.json
        file.write(data['motd'])
    return 'Success!'

app.run()

```

Run the application again

```
py app.py
```

Set route in Postman to

```
localhost:5000/setmotd
```

Set method in request to POST

Select Body, set type to raw and select JSON from the dropdown

Enter the following request body
```
{ "motd": "Great Job!"}
```

Send request

Review results

Set method back to GET and set route to

```
localhost:5000/motd
```

Send request

Review results

Congratulations on a non-zero day!

Resources:
HTTP Specification
https://tools.ietf.org/html/rfc7231
