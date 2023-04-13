# add fields to the User model in Django

## Create a project

```bash
django-admin startproject myproject
```

## Create a app

```bash
cd myproject
python manage.py startapp accounts
```

## models.py

```bash
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    pass
```

## settings.py

```py
INSTALLED_APPS = [
    ...
    ...
    'accounts', 
]
```

## add to the bottom file `settings.py`

```py
AUTH_USER_MODEL = 'accounts.CustomUser'
```

## makemigrations and migrate

```py
python manage.py makemigrations && python manage.py migrate
```

## File `models.py`

```py
from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    is_student = models.BooleanField(default=False)
    is_teacher = models.BooleanField(default=False)
    mailing_address = models.CharField(max_length=200, blank=True)
```

## File `admin.py`

```py
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    pass

admin.site.register(CustomUser, CustomUserAdmin)
```

Don't forget to also 'python manage.py createsuperuser' so you can access the admin

## Final `admin.py`

Use "password1" and "password2" in "fields" to create and confirm the password.

```py
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    list_display = (
        'username', 'email', 'first_name', 'last_name', 'is_staff',
        'is_teacher', 'is_student', 'mailing_address'
        )

    fieldsets = (
        (None, {
            'fields': ('username', 'password')
        }),
        ('Personal info', {
            'fields': ('first_name', 'last_name', 'email')
        }),
        ('Permissions', {
            'fields': (
                'is_active', 'is_staff', 'is_superuser',
                'groups', 'user_permissions'
                )
        }),
        ('Important dates', {
            'fields': ('last_login', 'date_joined')
        }),
        ('Additional info', {
            'fields': ('is_student', 'is_teacher', 'mailing_address')
        })
    )

    add_fieldsets = (
        (None, {
            'fields': ('username', 'password1', 'password2')
        }),
        ('Personal info', {
            'fields': ('first_name', 'last_name', 'email')
        }),
        ('Permissions', {
            'fields': (
                'is_active', 'is_staff', 'is_superuser',
                'groups', 'user_permissions'
                )
        }),
        ('Important dates', {
            'fields': ('last_login', 'date_joined')
        }),
        ('Additional info', {
            'fields': ('is_student', 'is_teacher', 'mailing_address')
        })
    )

admin.site.register(CustomUser, CustomUserAdmin)
```

## Run makemigrations and migrate

```py
python manage.py makemigrations && python manage.py migrate
```
