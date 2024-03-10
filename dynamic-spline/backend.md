---
description: Ürünler için bir model ve view yazıp buna endpoint yazdım.
---

# 🛣️ Backend

## Denemek için tam bu noktadan başla:

`git clone git@github.com:msdsn/Dynamic-Spline.git`

`git checkout b81e16fe0b56a7d944b92720cc9fb9d09dae7174`

[_kurulumu tamamla_](djangon-spline.md#backend-baslat)

***

## Model:

{% code title="api/models.py" %}
```python
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=255)
    brand = models.CharField(max_length=255)
    category = models.CharField(max_length=255)
    stock = models.IntegerField()

    def __str__(self):
        return self.name
```
{% endcode %}

{% code title="api/serializers.py" %}
```python
from .models import Product

from rest_framework import serializers

class ProductSerializer(serializers.HyperlinkedModelSerializer):
    class Meta:
        model = Product
        fields = ('name', 'brand', 'category', 'stock')
```
{% endcode %}

{% code title="api/views.py" %}
```python
from django.shortcuts import render
from rest_framework import viewsets

from .models import Product
from .serializers import ProductSerializer

class ProductViewSet(viewsets.ModelViewSet):
    queryset = Product.objects.all().order_by('name')
    serializer_class = ProductSerializer

```
{% endcode %}

{% code title="api/urls.py" %}
```python
from django.urls import path, include
from rest_framework import routers
from .views import ProductViewSet

router = routers.DefaultRouter()
router.register(r'products', ProductViewSet)


urlpatterns = [
    path('', include(router.urls)),
]

```
{% endcode %}

