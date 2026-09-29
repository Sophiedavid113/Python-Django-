Http method 
from django.http import HttpResponse

def hello_world(request):
    return HttpResponse("Hello World")
....................................................................
                       Url and routing
from django.urls import path
from .views import hello

urlpatterns = [
    path("hello/", hello),
]
....................................................................
                         Templates
from django.shortcuts import render

def home(request):
    return render(request, "home.html", {"name": "Ali"})
....................................................................
                            Model
from django.shortcuts import render
from .models import Student

def home(request):
    student = Student.objects.first()
    return render(request, "home.html", {"student": student})
....................................................................
               E-commerce model
 from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=100)
    price = models.IntegerField()
    description = models.TextField()
    image = models.ImageField(upload_to="products/")
    created_at = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.name
....................................................................
       Rest API front-end and back-end 
             back-end 
   # views.py
from rest_framework.response import Response
from rest_framework.decorators import api_view

@api_view(["GET"])
def products(request):
    data = [
        {
            "name": "Laptop",
            "price": 50000,
            "image": "laptop.jpg"
        },
        {
            "name": "Camera",
            "price": 30000,
            "image": "camera.jpg"
        }
    ]

    return Response(data)
....................................................................
                                 front-end 
<!DOCTYPE html>
<html>
<head>
    <title>Products</title>
</head>

<body>

<h1>Products</h1>

<div id="products"></div>

<script>
fetch("http://127.0.0.1:8000/api/products/")
    .then(response => response.json())
    .then(data => {

        data.forEach(product => {

            document.getElementById("products").innerHTML += `
                <div>
                    <img src="${product.image}" width="200">

                    <h2>${product.name}</h2>

                    <p>Price: ${product.price}</p>
                </div>
            `;

        });

    });
</script>

</body>
</html>
....................................................................





