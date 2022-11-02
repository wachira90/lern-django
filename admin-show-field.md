# admin show field

```
from django.contrib import admin
from .models import stocklist, datastock

class DatastockAdmin(admin.ModelAdmin):
    list_display = ('stock_name', 'date', 'open', 'high', 'low', 'close' )

admin.site.register(datastock, DatastockAdmin)
admin.site.register(stocklist)
```
