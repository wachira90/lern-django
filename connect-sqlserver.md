
# django connect sqlserver


````
pip install mssql-django

python3 -m pip install django mssql-django


django-admin startproject mysite


nano mysite/mysite/settings.py

# settings.py
DATABASES = {
    "default": {
        "ENGINE": "mssql",
        "NAME": "DATABASE_NAME",
        "USER": "USER_NAME",
        "PASSWORD": "PASSWORD",
        "HOST": "HOST_ADDRESS",
        "PORT": "1433",
        "OPTIONS": {"driver": "ODBC Driver 17 for SQL Server", 
        },
    },
}


python manage.py runserver
````

