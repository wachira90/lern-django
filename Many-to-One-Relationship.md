# Many to One Relationship

In django one to one and many to one relationship we use foreign key where one to one unique=true.

````
from django.db import models

class Teacher(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
    
    def __str__(self):
        return "%s %s" % (self.first_name, self.last_name)

class Publication(models.Model):
    title = models.CharField(max_length=100)
    pub_date = models.DateField()
    teacher = models.ForeignKey(Teacher, on_delete=models.CASCADE)

    def __str__(self):
        return self.title

    class Meta:
        ordering = ('title',)
````        
