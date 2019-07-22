# Django

*Model-Template-View* (MTV) Web development framework

Provides a HTTP server, an SQL connection and a template framework

| MVC naming | Django naming | Files |
| :-- | :-- | :-- |
| Model | Model | models.py |
| View | Templates | templates (multiple files - one for each page)
| Controller | Views | views.py |

## Setup

### Initialize repo

| Command | Description |
| :-- | :-- |
| `python3 -m venv env` | Set up the virtual environment |
| `source env/bin/activate` | Activate the virtual environment |
| `pip install django` | Install django in the virtual environment |


### Setup project

| Command | Description |
| :-- | :-- |
| `django-admin startproject my_site` | Initialize the django project |
| `python manage.py runserver` | Run the Django development server first time|
| `python manage.py migrate` | Setup/update the database for the Django project |


### Setup app

| Command | Description |
| :-- | :-- |
| `python manage.py startapp polls` | Initialize the app inside the local project |
| `python manage.py migrate` | Setup/update the database for the Django project |


### Register app

```py
INSTALLED_APPS = [
    'my_app.apps.my_appConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    ...
```

### Create models

```py
from django.db import models

class ClassName(models.Model):
    attribute = "value"

    def __str__():
        return "Meaningfull string describing the model"

    def custom_method():
        return "custom something"
```

### Routing

#### App
/site/app/urls.py
```py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('admin/', admin.site.urls),
```

#### Project
/my_site/urls.py
```py
...
from django.urls import include

urlpatterns = [
    path('polls/', include('polls.urls')),
    ...
```


#### Admin
/apps/admin.py

```py
from django.contrib import admin
from .models import ModelName

admin.site.register(ModelName)
```

### Views
/polls/views.py

```py
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```



# Dump

| | |
| :-- | :-- |
| `{% python script %}` | Python script |
| `{{ variable }}` | variable |


.all()
.get(pk=1)
.create


## Django buil in methods

.classname_set.

.delete
__





# 20181003

## Django

### Create project
| `django-admin startproject mysite` | Create project |
| `python manage.py runserver` | Run server |
| `python manage.py startapp polls` | Create app |



# 20181002







| `python manage.py makemigrations polls` | Create a snapshot of the current model state |

#### 2. Register app

```py
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'my_app.apps.my_appConfig',
]
```
#### 3. Register URLS



#### 4. Register views

```py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]

``

Then add functions to the views.py file inside the app folder. Each function correspond roughly to a page.

Add/register the name of the app to the /app/settings.py file under INSTALLED_APPS =

|  |  |
| :-- | :-- |
| `python manage.py runserver` | Run the Django development server |


python manage.py shell


### Routing

| site/urls.py | Routing for the site
| app/urls.py | Routing for the app


```py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')), # app url
    path('admin/', admin.site.urls), # admin url
]
```



### Changing the database

| Django | Database |
| :-- | :-- |
| model.py | database |
| class | table |
| variable | column |

### Committing changes to the database

|  |  |
| :-- | :-- |
| python manage.py makemigrations polls | |
| python manage.py sqlmigrate polls 0001) | See the changes |
| python manage.py migrate |


If you make changes to the model.py file, you have to run


### Populating the database

```py
my_question = Question(questions_text="What's up")
my_question.save()
```
Saves the text "What's up" to the questions_text column in the Questions table.

### Admin

|  |  |
| :-- | :-- |
| `python manage.py createsuperuser` | Create a superuser |




127.0.0.1:8000
