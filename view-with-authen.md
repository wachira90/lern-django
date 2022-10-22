# view with authen

````
from django.shortcuts import render
from django.template import loader
from .models import Servermon
from django.http import HttpResponse
from django.contrib.auth.decorators import login_required

@login_required
def index(request):
    latest_servermon_list = Servermon.objects.order_by('-created_at')[:5]
    template = loader.get_template('index.html')
    context = {
        'latest_servermon_list': latest_servermon_list,
    }
    return HttpResponse(template.render(context, request))
````    
