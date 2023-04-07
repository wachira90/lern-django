# django collectstatic

## file location

````
(env) django@test-imac:~/rest-test/appmain$ pwd
/home/django/rest-test/appmain
(env) django@test-imac:~/rest-test/appmain$ nano appmain/settings.py

````

## add to settings.py

````
import os
MEDIA_URL = '/media/'
STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static')

#STATICFILES_DIRS = [
#    os.path.join(BASE_DIR, 'static')
#]
#STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
````

python manage.py collectstatic


### nginx config

````
location /static {
    alias /home/django/rest-test/appmain/static;
    expires 7d;
}
````

## example 

python manage.py collectstatic

````
(env) django@test-imac:~/rest-test/appmain$ python manage.py collectstatic

You have requested to collect static files at the destination
location as specified in your settings:

    /home/django/rest-test/appmain/staticfiles

This will overwrite existing files!
Are you sure you want to do this?

Type 'yes' to continue, or 'no' to cancel: yes

0 static files copied to '/home/django/rest-test/appmain/staticfiles', 163 unmodified.
(env) django@test-imac:~/rest-test/appmain$
````
