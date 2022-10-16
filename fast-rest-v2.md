# Standard view method as REST service with parameters and different output formats

## urls.py (In stores app)

````
from coffeehouse.stores import views as stores_views

urlpatterns = [
    url(r'^rest/$',stores_views.rest_store,name="rest_index"),
    url(r'^(?P<store_id>\d+)/rest/$',stores_views.rest_store,name="rest_detail"),
]
````

## views.py (In stores app)

````
from django.http import HttpResponse
from coffeehouse.stores.models import Store
from django.core import serializers

def rest_store(request,store_id=None):
    store_list = Store.objects.all()
    if store_id:
        store_list = store_list.filter(id=store_id)
    if 'type' in request.GET and request.GET['type'] == 'xml':
        serialized_stores = serializers.serialize('xml',store_list)
        return HttpResponse(serialized_stores, content_type='application/xml')
    else:
        serialized_stores = serializers.serialize('json',store_list)
        return HttpResponse(serialized_stores, content_type='application/json')
````

## test 

````
/stores/rest/

/stores/rest/?type=xml
````
