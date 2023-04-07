# load env

##  Install Django Environ

```bash
pip install django-environ
```

##  Import environ in `settings.py`

```py
import environ
```

##  Initialise environ

```py
import environ
# Initialise environment variables
env = environ.Env()
environ.Env.read_env()
```

##  Create your `.env` file

In the same directory as `settings.py`, create a file called `.env`

##  Declare your environment variables in `.env`

```env
SECRET_KEY=xxxx
DATABASE_NAME=xxxx
DATABASE_USER=xxxx
DATABASE_PASS=xxxx
```

##  Replace all references to your environment variables in `settings.py`

```
DATABASES = {
  'default': {
    'ENGINE': 'django.db.backends.postgresql_psycopg2',
    'NAME': env('DATABASE_NAME'),
    'USER': env('DATABASE_USER'),
    'PASSWORD': env('DATABASE_PASS'),
  }
}

SECRET_KEY = env('SECRET_KEY')
```


#### `.gitignore` file already, create one at the project root Make sure the name of your `.env` file is included
