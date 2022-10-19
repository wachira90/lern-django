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
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static')
]
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
````

## example 

python manage.py collectstatic

````
(env) django@test-imac:~/rest-test/appmain$ python manage.py collectstatic
Traceback (most recent call last):
  File "manage.py", line 22, in <module>
    main()
  File "manage.py", line 18, in main
    execute_from_command_line(sys.argv)
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/core/management/__init__.py", line 419, in execute_from_command_line
    utility.execute()
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/core/management/__init__.py", line 413, in execute
    self.fetch_command(subcommand).run_from_argv(self.argv)
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/core/management/base.py", line 354, in run_from_argv
    self.execute(*args, **cmd_options)
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/core/management/base.py", line 398, in execute
    output = self.handle(*args, **options)
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 187, in handle
    collected = self.collect()
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/contrib/staticfiles/management/commands/collectstatic.py", line 105, in collect
    for path, storage in finder.list(self.ignore_patterns):
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/contrib/staticfiles/finders.py", line 130, in list
    for path in utils.get_files(storage, ignore_patterns):
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/contrib/staticfiles/utils.py", line 23, in get_files
    directories, files = storage.listdir(location)
  File "/home/django/rest-test/env/lib/python3.7/site-packages/django/core/files/storage.py", line 330, in listdir
    for entry in os.scandir(path):
FileNotFoundError: [Errno 2] No such file or directory: '/home/django/rest-test/appmain/static'
(env) django@test-imac:~/rest-test/appmain$ mkdir /home/django/rest-test/appmain/static
(env) django@test-imac:~/rest-test/appmain$ python manage.py collectstatic

163 static files copied to '/home/django/rest-test/appmain/staticfiles'.
(env) django@test-imac:~/rest-test/appmain$ mkdir /home/django/rest-test/appmain/staticfiles
mkdir: cannot create directory ‘/home/django/rest-test/appmain/staticfiles’: File exists
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
