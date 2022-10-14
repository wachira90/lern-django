# REST GET START

## ENVIRONMENT SETTING

````
mkdir rest-test/

cd rest-test/

python -m venv env

### WINDOWS
env/Scripts/activate

### LINUX
source env/bin/activate
````
## INSTALL PACKAGE

````
pip install django djangorestframework

django-admin startproject appmain

cd appmain/

python manage.py startapp appsubapi
````

## SETTING 

````
nano appmain/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'appsubapi',  # Oup app
    'rest_framework'  # DRF
]
````

### nano appsubapi/models.py

````
from django.db import models

class Task(models.Model):
    title = models.CharField(max_length=80)
    description = models.TextField()
    date_created = models.DateTimeField(auto_now_add=True)
    complete = models.BooleanField()

    class Meta:
        ordering = ['-date_created']
        db_table = 'task'
    
    def __str__(self):
        return self.title
````


## MIGRATE
````
python manage.py makemigrations && python manage.py migrate
````

### nano appsubapi/serializers.py


````
from rest_framework import serializers
from .models import Task

class TaskSerializer(serializers.ModelSerializer):

    class Meta:
        model = Task
        fields = ('id', 'title', 'description', 'date_created', 'complete')
````

### nano appsubapi/views.py


````
from django.shortcuts import render
from .serializers import TaskSerializer
from .models import Task
from rest_framework import generics

class TaskList(generics.ListAPIView):
    queryset = Task.objects.all()
    serializer_class = TaskSerializer
    permission_classes = [permissions.IsAuthenticated]
    # return Response(queryset.data)

class TaskDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Task.objects.all()
    serializer_class = TaskSerializer
    permission_classes = [permissions.IsAuthenticated]

# add data
class TaskList(generics.ListCreateAPIView):
    queryset = Task.objects.all()
    serializer_class = TaskSerializer
    permission_classes = [permissions.IsAuthenticated]
````

### nano appmain/urls.py

````
from django.contrib import admin
from django.urls import path, include
from api import views

urlpatterns = [
#    path('', include('rest_framework.urls')),
    path('admin/', admin.site.urls),
    path('api/tasks/', views.TaskList.as_view()),
    path('api/tasks/<int:pk>', views.TaskDetail.as_view()),
    path('api-auth/', include('rest_framework.urls')),
]
````

## API LIST

````
/api/tasks/  -->  GET --> ดึงข้อมูล tasks มาแสดงผลทุก task
/api/tasks/<id>/   -->  GET  --> ดึงข้อมูลมาแสดงเฉพาะ task นั้น ๆ 
/api/tasks/   -->  POST  --> สร้าง task ขึ้นมาใหม่
/api/tasks/<id>/   -->  PUT  --> อัปเดตข้อมูลใน task นั้น ๆ  
/api/tasks/<id>/   -->  DELETE  --> ลบ task นั้น ๆ  
````

## MIGRATE
````
python manage.py makemigrations && python manage.py migrate
````

### nano appmain/settings.py

````
ALLOWED_HOSTS = ['*']
````

## ADD USER ADMIN
````
python manage.py createsuperuser --email admin@example.com --username admin

python manage.py createsuperuser --email wachira@example.com --username wachira
````

### nano appsubapi/admin.py

````
from django.contrib import admin
from .models import Task

# Register our model
admin.site.register(Task)

````

## RESULT

````
python manage.py runserver 0.0.0.0:8001

http://127.0.0.1:8001/api/tasks/

http://172.16.1.5:8001/api/tasks/

````





