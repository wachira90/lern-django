# rest_framework

## create project

````
python -m pip install --upgrade pip

pip install virtualenv

python -m venv env

(windows)
.\env\Scripts\activate

(linux)
source .\env\bin\activate

pip install django djangorestframework

django-admin startproject tutorial

cd tutorial

django-admin startapp quickstart

python manage.py migrate

python manage.py createsuperuser --email admin@example.com --username admin
````

## create tutorial/quickstart/serializers.py

````
from django.contrib.auth.models import User, Group
from rest_framework import serializers

class UserSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = User
        fields = ['url', 'username', 'email', 'groups']

class GroupSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Group
        fields = ['url', 'name']

````        


## add tutorial/quickstart/views.py

````
from django.contrib.auth.models import User, Group
from rest_framework import viewsets, permissions
from quickstart.serializers import UserSerializer, GroupSerializer


class UserViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows users to be viewed or edited.
    """
    queryset = User.objects.all().order_by('-date_joined')
    serializer_class = UserSerializer
    permission_classes = [permissions.IsAuthenticated]


class GroupViewSet(viewsets.ModelViewSet):
    """
    API endpoint that allows groups to be viewed or edited.
    """
    queryset = Group.objects.all()
    serializer_class = GroupSerializer
    permission_classes = [permissions.IsAuthenticated]
````



## add tutorial\tutorial\urls.py

````
from django.contrib import admin
from django.urls import include, path
from rest_framework import routers
from quickstart import views

router = routers.DefaultRouter()
router.register(r'users', views.UserViewSet)
router.register(r'groups', views.GroupViewSet)

# Wire up our API using automatic URL routing.
# Additionally, we include login URLs for the browsable API.
urlpatterns = [
    path('', include(router.urls)),
    path('sadmin/', admin.site.urls),
    path('api-auth/', include('rest_framework.urls', namespace='rest_framework'))
]
````


## add tutorial/settings.py

````
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
````

````
INSTALLED_APPS = [
    ...
    'rest_framework',
]


ALLOWED_HOSTS = ['localhost','127.0.0.1']
````

### add option 
````
APPEND_SLASH=True

CACHES = {
    'default': {
        # 'BACKEND': 'django.core.cache.backends.dummy.DummyCache',
        'BACKEND': 'django.core.cache.backends.locmem.LocMemCache',
        'LOCATION': 'unique-snowflake',
    }
}
````

## test run
````
python manage.py runserver
````

## test curl
````
C:\Users\admin>curl -H "Accept: application/json; indent=4" -u admin:admin http://127.0.0.1:8000/users/
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "url": "http://127.0.0.1:8000/users/1/",
            "username": "admin",
            "email": "admin@example.com",
            "groups": []
        }
    ]
}
C:\Users\admin>
````
