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
