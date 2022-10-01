
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

