
## Virtual environment
| | |
| :-- | :-- |
| `python3 -m venv env` | Set up venv |
| `source env/bin/activate` | activate venv |
| `pip install --upgrade pip` | Upgrade pip |

## Django file structure
| | |
| :-- | :-- |
| `pip install django` | install django |
| `django-admin startproject {projectname}` | Starts django project and creates file structure |
| `cd {projectname}` | Move into the projectfolder where the manage.py file is|
| `python manage.py startapp {app_name}` | Create Django app |

## Git
| | |
| :-- | :-- |
| `git init` | initialize git |
| `touch .gitignore` | Create gitignore file  |
| `vim .gitignore` | Add env etc to gitignore file |
| `pip freeze > requirements.txt` |
| `git add .` | add all files to git |

## Settings
Add the path to the name of the app to `my_app/settings.py` under the `INSTALLED_APPS` section.
```py
INSTALLED_APPS = [
    'my_app.apps.MyAppConfig',
    'django.contrib.admin',
```
Copy the SECRET_KEY from the settings file. Add it to your env/bin/activate file as an export
```
export DJANGO_SECRET_KEY='{your key}'
```
and add the following to the deactivate section:
```
...
deactivate () {

        unset DJANGO_SECRET_KEY
...
```
Save and exit the activate script and navigate to the folder with the manage.py script in your Django project

Run Server and make migrations
```
python manage.py migrate
python manage.py makemigrations
python manage.py runserver
```
Visit `http://127.0.0.1:8000/` and get an "installed successfully" message.

## Map the paths to the app





| | |
| :-- | :-- |



Create app
Register app in settings.py (get name from apps.py)
Set up url patterns in project/urls.py - path('root/', include('app_name.urls')),
Set up
