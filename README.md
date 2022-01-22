# Table of contents

* [Flask Web Server](#flask-web-server)


# Deploy a Web Server on Heroku with Flask

Flask Web Server
============

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
```python
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
- Before deploying the project in Heroku we have to create some folders for dependecies
- Create a file with name Procfile and copy the code below and paste it
```
web: gunicorn  main:app
```
- Create runtime.txt and write which python version you are using in it, in my app I'm using python 3.9.7
```
python-3.9.7
```
- Now we have to define requirements, open the terminal in project file and write the code below
```
pip freeze > requirements.txt
```
## Heroku
- Firstly you have to install Heroku CLI, you can follow that link to install Heroku CLI : https://devcenter.heroku.com/articles/heroku-cli
- Then you have to install git on your system, you can follow the link : https://git-scm.com/
- Then after, open the terminal in project file then copy the codes below one by one
```
heroku login
```
- You can change the play-Ard section with whatever you want
```
heroku create play-Ard --buildpack heroku/python
```
- Then, initialize the git
```
git init
```
```
git add .
```
```
git commit -m "Flask-playArd"
```
```
heroku git:remote -a play-Ard
```
- If you come here with no error, we can finally deploy our project to Heroku 
```
git push heroku master
```
- This project live in https://play-ard.herokuapp.com/questions/, you can visit
