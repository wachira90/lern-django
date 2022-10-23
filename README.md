# lern-django
lerning django

python 3.7

django 3.2

## init project init1.bat

````
@ECHO ON 
python -m venv env
# OR
virtualenv --python="/usr/bin/python2.6" env
# OR
virtualenv env

# WINDOWS
env\Scripts\activate

# LINUX
source env\bin\activate
````

## init project init2.bat

````
@ECHO ON
pip install django
pip install djangorestframework
django-admin startproject appmain
CD appmain
python manage.py startapp api
python manage.py runserver 0.0.0.0:8000

````

## install package
````
pip install -r requirements.txt
````

## freeze package
````
pip freeze > requirements.txt
````

## setting 
````
TIME_ZONE = 'Asia/Bangkok'
````


## command 
````
python manage.py makemigrations && python manage.py migrate

python manage.py createsuperuser --email admin@example.com --username admin

python manage.py runserver 0.0.0.0:8000

pip install mysqlclient==1.4.6   (if error [sudo apt install libmysqlclient-dev -y])
````


## LOOP CYCLE

````

# CREATE_MODEL
appmain\api\models.py


# REGISTER 
appmain\api\admin.py


# SERIALS LIST FILED
appmain\api\serializers.py


# VIEW
appmain\api\views.py


# URL CREATE PATH 
appmain\appmain\urls.py
````


## Logging

appmain\settings.py

````
import logging
logging.disable(logging.CRITICAL)

# logging.disable(logging.NOTSET)
````
