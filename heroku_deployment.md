STEPS:
UPLOAD YOUR CODE TO GITHUB
LOGIN TO HEROKU AND CREATE A NEW APP
GO TO DEPLOY TABS AND UNDER DEPLOYMENT METHOD CLICK ON GITHUB SINCE THAT IS WHERE OUR CODE LIES
AFTER THAT SELECT OUR PROJECT AND LINK IT TO HEROKU ON THIS SAME CONFIGURATION SETTINGS
AFTER THAT CREATE YOUR REQUIREMENTS.TXT FILE CONTAINING ALL THE LIBRARIES RO RUN THE APP
THE CREATE A RUNTIME.TXT FILE CONTAINING THE PYTHON VERSION TO THE APP
AND THEN CREATE UWSGI.INI AND PUT THE NECESSARY CONFIGURATION

AFTER THAT, WE THEN CREATE A RUN.PY FILE AND IMPROT OUR APP FOR EXAMPLE THIS CONFIGURATION BELOW

from app import app
from db import db

db.init_app(app)

@app.before_first_request
def create_tables():
    db.create_all()



HOW TO VIEW ERROR LOGS
do heroku login, and you will be automatically login,
then do
heroku logs --app=investcryptoapp --tail