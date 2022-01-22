# Deploy a Web Server on Heroku with Flask

## Flask Web Server

### Creating a virtual environment for Flask requirements

- Create a directory with the name you want
- Then open the cmd and print 
```
 virtualenv venv
```
- If you are using Windows you can activate the virtual environment with that command
```
venv\Scripts\activate.bat
```
### Installing Libraries
- Now you have to insall Flask, Flask-RESTful and gunicorn for server
```
pip install Flask
pip install flask-restful
pip install gunicorn
```
- One more libraries for Flask Core
```
pip install Flask-Cors
```
### Creating a Flask App
- Then create a main.py file, copy the code below and paste in it.
```
from flask import Flask, jsonify
from flask_restful import Resource, Api
from flask_cors import CORS

app = Flask(__name__)
api = Api(app)
CORS(app)

questions = {"questions":"Turkiyenin en buyuk dagi?","answers":'Agri Dagi'}

class status (Resource):
    def get(self):
        try:
            return {'data': 'Api is Running'}
        except:
            return {'data': 'An Error Occurred during fetching Api'}

class Questions(Resource):
    def get(self):
        return jsonify(questions)


api.add_resource(status, '/')

api.add_resource(Questions, '/questions/')

if __name__ == '__main__':
    app.run()
```


