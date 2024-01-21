# Notes

## folder
- init tells django to use as a package
- asgi and swgi are special config files, allows django to comm with web server
- settings: config based
- urls: route to different apps
- manage: acts as a command line tool

## w3 schools
Set up virtual environment:
- python3 -m venv <virtual environment name>
- To activate environment run: source <myenv name>/bin/activate
- Install django: python3 -m pip install Django
    - check version django-admin --version
- django-admin startproject <project name> . -- Add the period to make at current dir
    - add string name of app in installed apps under settings.py to connect the add> 
- (if not current directory) cd to project, run: python3 manage.py runserver <can specify server port>
    - check by clicking on Starting development server at http://127.0.0.1:8000/, will return a success site
    - NOTE: manage.py is a django-admin wrapper

Set up App:
- to create a new app python3 manage.py startapp <app name>

Render HTML:
- in views add from django.http import HttpResponse
    - write function that uses HttpResponse
- create a urls.py in that folder
    - include : from django.urls import path
                from . import views
    - will need to include: urlpatterns = [
        path('members/', views.members, name='members'),
    ]
- nav to main project urls.py folder include: from django.contrib import admin
                                              from django.urls import include, path
    - file will need a matching: urlpatterns = [
        path('', include('members.urls')),
        path('admin/', admin.site.urls),
    ]
- run server to check: python3 manage.py runserver

Django Templates:
- create a templates folder in <app> directory
- add html.index
- views in app should look like: 
    from django.http import HttpResponse
    from django.template import loader

    def members(request):
    template = loader.get_template('myfirst.html')
    return HttpResponse(template.render())
- make sure app <name> is listed in settings
- run: python3 manage.py migrate
- python3 manage.py runserver

Django Models:
- Go to app models.py and create a class
- Ex:
    from django.db import models

    # Create your models here.
    class Member(models.Model):
        firstname = models.CharField(max_length=255)
        lastname = models.CharField(max_length=255)
- This ex is using sqlite
- run to create migration: python3 manage.py makemigrations <app name>
- run to execute migration: python3 manage.py migrate
- view sql statement: python3 manage.py sqlmigrate members 0001