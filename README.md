# lern-django
lerning django

## init project init1.bat

````
@ECHO ON 
python -m venv env
env\Scripts\activate
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
