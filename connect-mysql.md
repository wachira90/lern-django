
# django connect mysql


````
pip install mssql-django

python3 -m pip install django mysqlclient


django-admin startproject mysite


nano mysite/mysite/settings.py

# settings.py

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'djangodatabase',
        'USER': 'dbadmin',
        'PASSWORD': '12345',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}


python manage.py runserver
````

## install mysqlclient 

````
https://www.lfd.uci.edu/~gohlke/pythonlibs/#mysqlclient

pip install mysqlclient-1.4.6-cp37-cp37m-win_amd64.whl
````


