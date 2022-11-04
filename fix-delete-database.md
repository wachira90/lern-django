# fix-delete-database

delete all the migrations files from migration folder 

python manage.py makemigrations appname

python manage.py migrate  

```
(env) C:\Users\admin\Desktop\project-masterstock\masterstock>python manage.py makemigrations && python manage.py migrate
No changes detected
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  No migrations to apply.

(env) C:\Users\admin\Desktop\project-masterstock\masterstock>python manage.py makemigrations api
Migrations for 'api':
  api\migrations\0001_initial.py
    - Create model datafinance
    - Create model datastock
    - Create model stocklist

(env) C:\Users\admin\Desktop\project-masterstock\masterstock>python manage.py migrate
Operations to perform:
  Apply all migrations: admin, api, auth, contenttypes, sessions
Running migrations:
  Applying api.0001_initial... OK

(env) C:\Users\admin\Desktop\project-masterstock\masterstock>
```
