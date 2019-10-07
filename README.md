# creating-a-landing-page-Using-Django
Python css and Html 

Creating a Django project
I will assume you have Django installed but in case you don’t, you can use the official installation guide.

To create a project run the following command in your terminal

django-admin startproject mun
And after the project is created go to its directory via cd command

cd /mun
And starting a server is as simple as

python manage.py runserver
After visiting 127.0.0.1:8000 you should see a screen that everything is great…

Django default landing page

Except it’s not your landing page…





Where do we start?
To add a landing page we need to create an “app” which is a Django concept for things that are not coupled to your app and can be extracted from it (for example authentication which can be used in other applications too).

But let’s not get into that too much and just create a simple app called “pages” which will only contain static pages like “landing”, “contact us” and “about”.

python manage.py startapp pages
When the app is ready, we need to add it to Django’s INSTALLED_APPS. We’ll Just append our app to the end of those other ones because we’re going to need some of those.






INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'pages',
]





The newly created pages app has a new pages folder with a couple of python files. Particular ones that interest us are pages/urls.py and pages/views.py.

URLs
When a request comes to the server, Django has to find a “view”, a function that will process the request and send the response. The way Django finds how to connect a URL that came with the request and a view is via urlpatterns which are located in your project’s main directory. In my case, it’s mun/urls.py.

In order to show our landing page on 127.0.0.1:8000 and essentially on our main domain we need to add the following code to pages/urls.py

from django.urls import path
from . import views

urlpatterns = [
	path('', views.index, name='index'),
]
A path is what comes after a domain in a URL. For example, in the URL https://www.google.com/search?q=mun the path would be /search?q=mun. Since we want our landing page to be on the / path the first parameter we provide to the path method is ''. The second argument is what view we need to render which is an index view in our case.

We also need to add urlpatterns from our app to the main project’s urlpatterns with a built-in function include

from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('', include('pages.urls')),
    path('admin/', admin.site.urls),
]
