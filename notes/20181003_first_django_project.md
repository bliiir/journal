### Journal
*Rasmus Groth, Barcelona, Spain, 20181003*

# Django
As part of the CodingNomads, Python course, we are learning how to work with Django. In order to absorb the knowledge, I have written this tutorial for myself. It is an almost exact copy of the really good one found at [djangoproject.com](
https://docs.djangoproject.com/en/2.1/intro/tutorial01/)

Django is what you would end up with after a few years of coding dynamic python based websites up that are running on databases and you had built out your own classes and methods to deal with database operations, routing and dynamic HTML production. <sup>[1](#footnote_0001)</sup>


## Setup steps
Note: I am assuming you have python 3.x, pip and virtual environments installed already. If not follow [these instructions](https://docs.python-guide.org/starting/install3/osx/).

First we'll setup the folder structure and virtual environment.

### Initialize repo

| Command | Description |
| :-- | :-- |
| `python3 -m venv env` | Set up the virtual environment |
| `source env/bin/activate` | Activate the virtual environment |
| `pip install django` | Install django in the virtual environment |

### Setup project
Then we set up the project structure in Django

| Command | Description |
| :-- | :-- |
| `django-admin startproject my_site` | Initialize the django project |
| `python manage.py runserver` | Run the Django development server first time|
| `python manage.py migrate` | Setup/update the database for the Django project |

### Setup app
In this tutorial we are going to be working with a poll app - as in asking users questions and counting the anwswers. So, lets Initialize the app and update the database (will come back to this later):

| Command | Description |
| :-- | :-- |
| `python manage.py startapp polls` | Initialize the app inside the local project |
| `python manage.py migrate` | Setup/update the database for the Django project |

### Routing

Before we can make any URLS point to actual html in the browser, we have to tell Django how to interpret urls. First task is to tell Django that we have a polls app in the top level urls.py file

*my_site/urls.py*

```py
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```

Next, I have to have routing for my polls app. I create a new file in the `/polls` folder called `urls.py`.

*my_site/polls/urls.py*
```py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
]
```

This creates a base routing setup with a single valid view/page - the `index.html` file. An http request with an empty path will be redirected to to views.index which can be referenced using the string 'index'

With the routing out of the way, we are almost ready to launch our very first Django page. Let's go ahead and make the first view.


### First view

Open the `/polls/views.py` file and replace the content with the following:

*/polls/views.py*

```py
from django.http import HttpResponse

def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```
This creates a 'view' (page) that can be accessed via `/polls/index.html` or just `/polls`

Alright - almost ready to go. Go to terminal and run `python manage.py migrate` to update the database and then start the server again with the `python manage.py runserver` command. If it was running already, you will have toe terminate the process (ctrl+c on mac) and restart it using `python manage.py runserver`.

Great - now go to your browser and try:

```
http://127.0.0.1:8000/polls/
```

This should give you a page that says

> Hello, world. You're at the polls index.

---

# 🙌
**Yay!** You have published your first view using Django!

---

A little note on the `polls/urls.py` file

In the urlpatterns below:
```py
urlpatterns = [
    path('', views.index, name='index'),
]
```
The structure is as follows:

```
path(route, view, kwargs, name)
```
## Database and models

### Database Setup
If you want to change your database from sqlite, change the timzone etc, you do that in the `/my_site/settings.py` file as described [here](https://docs.djangoproject.com/en/2.1/intro/tutorial02/) - but you don't have to right now if you just want to try making a few pages with Django.

### Models
In Django the data handling part of the framework is called Models. In our case i simply means - the bits that read from the database and write to the database.

If you open up the `/polls/models.py` file it looks like this:

```py
from django.db import models

# Create your models here.
```
And it doesn't really do anything.

The tutorial is about

```py
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
What this does is create two tables: `Question` and `Choice` in our polls app.

Cool - so now, we have to tell Django that there is an app called `polls`. We do that in settings by adding `'polls.apps.PollsConfig'` to the `INSTALLED_APPS` section - like this:

```py
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```
Django still doesn't know though.

Next we (optionally?) create a kind of snapshot of the models by running the command `python manage.py makemigrations polls`. This creates a python file describing the models inside the `polls/migrations` folder.

Then we do the actual migrate - apply the changes to the models by using the command `python manage.py migrate`. This executes a long SQL statement that updates/creates the database.

# 👍
Awesome. We now have a database and we can play around with it by running the `python manage.py shell`


---

Ok, lets try writing to the database

```py
from polls.models import Choice, Question  # Make the Choice and Question models available
from django.utils import timezone  # Import the timezone module
```

Lets get a list of all the rows in the Question model/table
```py
Question.objects.all()  # SELECT * FROM Choice
```
    <QuerySet []>

Empty - we haven't written anything yet. Let's do that now:

```py
q = Question(question_text="What's new?", pub_date=timezone.now())
```
Instantiates the `Question` class as q and passes `"What's new?"` as an argument to `question_text` and `timezone.now()` to `pub_date` - the effect of which is to write a new row in the database with the SQL statement:

```sql
INSERT INTO question (question.question_text, question.pub_date) VALUES ("What's new?", timezone.now())
```
But it is only attributes of the model at this time and has not been saved to the database itself. We do that with:

```py
q.save()
```
Now we can do the `SELECT * FROM ...`

```py
Question.objects.all()
```
```
<QuerySet [<Question: Question object (1)>]>
```
Or we can do the equivalent of `SELECT question_text FROM question WHERE id=1`
```py
q.question_text
```
```
"What's new?"
```
We can assign a new value to the `question_text` of `q`:

```py
q.question_text = "What's up?"
q.save()
```
Try it again...
```py
q.question_text
```
```
"What's up?"
```
Django says to add __str__ methods to the models. Mine looks like this now:
```py
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def __str__(self):
        return self.question_text


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def __str__(self):
        return self.choice_text
```

Like any other function, you can add add custom methods to your classes in Django. Here is one that returns true if the Question was published within one day from the current time in the timezone set in the settings file.

```py
from django.db import models
import datetime
from django.utils import timezone


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')

    def __str__(self):
        return self.question_text

    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)

    def __str__(self):
        return self.choice_text
```
If we enter an interactive session with `python manage.py shell`, we can try the new functionality:

```py
from polls.models import Choice, Question
Question.objects.all()
```
```
<QuerySet [<Question: What's up?>]>
```
We now get the content of `question_text` returned when we query list all the objects of that class.




















# Footnotes

<a name="footnote_0001">1</a>:
Django is an [MVC](https://en.wikipedia.org/wiki/Model%E2%80%93view%E2%80%93controller) (Model, View, Controller) framework, but `Controller` is called `Views` and `Views` to `Templates` in Django. Model is the same... ish 🙄

| MVC | | Django | |
| :-- | :-- | :-- | :-- |
| M | Model | M | Model |
| V | View | T | Templates |
| C | Controller | V | Views |
