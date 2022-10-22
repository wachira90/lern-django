# static file


Check Your path again,

If it's correct Follow the Guidelines to Include CSS in Django Project

Static files are intended to wrap CSS files and your images, Django automatically identifies this file.

1. Create `static` folder in your `app` folder, same directory as of migrations and template folder

2. Create `css` Folder and insert it into static Folder

3. Now put your `styles.css` into `css` folder

4.Now in your HTML File where you want to include CSS, add `{% load static %}` On the top of HTML File and Your Path should be like this `<link rel="stylesheet" href="{% static 'css/styles.css' %}">` in HTML file.

5.Then Make Change To Your settings.py in projectfoldername with-

````
STATIC_URL = '/static/'
STATICFILES_DIRS = [ os.path.join(BASE_DIR,'static') ]
STATIC_ROOT = os.path.join(BASE_DIR, 'assets')
````

Then Run this command

````
python manage.py collectstatic
````

You static file will be copied to New file created by django as assets.


https://django.readthedocs.io/en/3.2.x/howto/static-files/index.html


