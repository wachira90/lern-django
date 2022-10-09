# disable browse api

django rest framwork disable browse api 

### nano appmain\appmain\settings.py

````
REST_FRAMEWORK = {
    'DEFAULT_RENDERER_CLASSES': (
        'rest_framework.renderers.JSONRenderer',
    )
}
````


### Per-view basis:

````
class MyView(...):
    renderer_classes = [renderers.JSONRenderer]
````    
