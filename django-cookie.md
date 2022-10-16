# django cookie

## views.py

````
from django.http import HttpResponse

def setcookie(request):
    cookie = "onlinetutorial"
    response = HttpResponse("Cookies Set with value "+cookie)   
    response.set_cookie('onlinetutorial', 'Protutorislplus.com')
    return response


def getcookie(request):
    getvalue = request.COOKIE['onlinetutorial']
    return HttpResponse("Welcome to "+getvalue);
````    
    
## urls.py

````
from django.contrib import admin
from django.urls import path

from helloworld import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.index, name="homepage"),
    path('setcookie', views.setcookie),
    path('getcookie', views.getcookie)
]
````


## templates/index.html

````
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Django Cookies</title>

</head>
<body>
 <h1>Django Cookies Tutorial</h1>
<Ul>
    <li><a href="/setcookie">SetCookie</a></li>
    <li><a href="/getcookie">Getookie</a></li>
</Ul>ul
</body>
</html>
````

## run server
````
python manage.py runserver

````
