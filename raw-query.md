# raw query

## views.py

```py
from django.db import connection

def raw(self):
    with connection.cursor() as cursor:
        # cursor.execute("UPDATE bar SET foo = 1 WHERE baz = %s", [self.baz])
        cursor.execute("SELECT eid, ename, euser, sta FROM e_tb LIMIT 5;")
        # row = cursor.fetchone()
        row = cursor.fetchall()

    return HttpResponse(row)
```    
