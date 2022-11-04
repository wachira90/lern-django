# models multiply field

Define a @property in model and access it from template as any other model field,


```
class ImpactMatrix(models.Model):
    objectName = models.ForeignKey(ObjectName, on_delete=models.CASCADE)
    actionName = models.ForeignKey(ActionObject, on_delete=models.CASCADE)
    priority = models.ForeignKey(Priority, on_delete=models.CASCADE, related_name='priority')
    functional = models.ForeignKey(Priority, on_delete=models.CASCADE, related_name='functional')
    supervision = models.ForeignKey(Priority, on_delete=models.CASCADE, related_name='supervision')
    approval = models.ForeignKey(Priority, on_delete=models.CASCADE, related_name='approval')

    @property
    def some_name(self):
        return self.priority.priorityScore*self.functional.priorityScore
        
```

and in your tempate,

```
{% impactmatrix_object.some_name %}
```
