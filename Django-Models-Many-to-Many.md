# Django Models Many to Many Relationship Example

Django manytomany field is similar to mysql join table.

````
from django.db import models

class Publication(models.Model):
    title = models.CharField(max_length=30)

    class Meta:
        ordering = ('title',)

    def __str__(self):
        return self.title

class Book(models.Model):
    headline = models.CharField(max_length=100)
    publications = models.ManyToManyField(Publication)

    class Meta:
        ordering = ('headline',)

    def __str__(self):
        return self.headline
````
