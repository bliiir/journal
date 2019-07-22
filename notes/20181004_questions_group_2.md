# QUESTIONS TO ANSWER FOR STUDENTS

Split up in groups of two/three and research and answer
common questions related to Django and Web Development.

After 2 hours of research time, you'll present the results
to the rest of the class.

----------------------------------------------------------


* What does python's `__init__.py` file do? Why is it used in Django?

    > When there is an __init__.py file inside a folder, that folder can be referenced as a package in an import statement in Python.

    > Example of use in Django:

    >    `from . import views`

    >Imports the `views.py` file in the `/polls` folder which has an `__init__.py` file

* What are HttpRequest and HttpResponse objects in Django? How do they differ from HTTP requests/responses?

    > HTTP requests/responses are character strings passed to a server via the HTTP protocol.

    > In Django, HttpRequest is formatted in a specific way and passed to the view which then returns a HttpResponse


* What is TDD (Test-driven development)? What's the advantage of using it?

    > TDD is a process where you write tests before you write code. You then iterate over the code until it passes the test.

    > The advantage is that each piece of code is created to solve a very specific task and as a dev you are not fiddling around with a vague spec.


* What is a "project" in Django, what are "apps"? Which metaphors related to other programming concepts can you come up with?

    > Projects are usually a full 'site' related to a domain - it bit.io. It contains the homepage, blog etc under it.
    Apps are subsets of the site - for example landing page, a blog, news, or documentation

    > Metaphors:
        > Project vs App,
        > Class vs method,
        > Class vs attribute

* What is a CSRF token and how does it work?

    > The CSRF protects against Cross Site Request Forgeries.

    > When you visit a page in your browser, the site adds a random token to the the request. For you to interact with the site, this token has to be correct. A malicious site will not be able to submit a correct token even if they have your login details. You get a new token for every request you make on the site - including reloading the page.


* What does registering an app in `INSTALLED_APPS` achieve?

    > It can be referenced elsewhere in Django - for example by the admin dashboard. If it isn't registered, the project does not know the app exists.

* What is the class Meta: construct in Django classes (e.g. Models and Serializers)?

    > The Meta class allows you to add metadata to models (database tables) or serialised formats - things that aren't actually in the database/file but might be useful to know or use - like organizing the data you are working with - for example default ordering, filtering etc.

* What is `reverse()` about in Django?

    > It You can store your current url in reverse so that if the user wants to go back, you can go back by calling reverse as the url

* What is a good way to debug Django apps during production?

    > You can use regular PDB as in other Python scripts


* What are Django's `generic` views? Which common ones exist and what can they be used for?

    > They are controller template classes. Examples: FormView, DetailView...

    > https://docs.djangoproject.com/en/2.1/ref/class-based-views/generic-editing/#formview

* What happens behind the scenes of the Django ORM?

    > Django maps primary and foreign keys in many-to-one relationships and creates lookup tables in many-to-many relationships automatically


* How does a database such as MySQL differ from SQLite (standard in Django)?

    > MySQL runs a persistent server. Sqllite is filebased and has not server running

* What happens when you run `python manage.py makemigrations`?

    > Django makes a snapshot of the current state of your models so that you can roll back or rebuild your models and db at any time in the future

* How do you correctly remove one app from a Django project without impacting the data provided by other apps?

    > You do a lot of grunt work:

    > Remove from INSTALLED_APPS in settings, tables in Models...

    > https://stackoverflow.com/questions/11382734/how-to-delete-an-app-from-a-django-project
