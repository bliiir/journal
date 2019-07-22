| Coding journal |  |
| :-- | :-- |
| Author | [Rasmus Groth](https://github.com/bliiir) |
| First entry | 20190125, Utterslev, Copenhagen, Denmark |
| Last entry | 20190125, Utterslev, Copenhagen, Denmark |


# TLDR

    pip install --upgrade pip -U
    git init
    git remote add origin https://github.com/{user}/{repo}.git
    $ python3 -m venv {virtual_environment_name}
    pip install -r requirements.txt
    pip3 install {package}
    pip3 install -U $(pip3 freeze | awk '{split($0, a, "=="); print a[1]}')
    pip freeze > requirements.txt
    vim env/bin/activate
    ...
    source env/bin/activate

Go!

---

# Setting up your python project

## Bring system up to date

Make sure you have the latest version of Python and then upgrade the Python package manager:

    $ pip install --upgrade pip -U

## Version control
Then navigate to the folder you want to work in - your project "home" folder and install git:

    git init

Now add your remote:

    git remote add origin https://github.com/{user}/{repo}.git

Now you are git versioned :)

### Virtual environment
Ok, next is setting up your virtual environment

    $ python3 -m venv {virtual_environment_name}

It is common to use the name `env`

If you have a requirements.txt file to install packages from, install from that now:

    pip install -r requirements.txt


If you have additional packages you want to install - or no requirements.txt, then install your packages now - for example:

    pip3 install pandas

Make sure you have the latest packages:

    pip3 install -U $(pip3 freeze | awk '{split($0, a, "=="); print a[1]}')

Now freeze the requirements again:

    pip freeze > requirements.txt

### Environment variables

Open env/bin/activate with vim:

    vim env/bin/activate

Add your environment variables to the activate script. First add “unset” of your variable names at the deactivate() module. I am using Twitter API keys as example here - it could be anything you want to be able to reference in your code.

```
deactivate () {
   unset TWITTER_API_KEY
   unset TWITTER_API_SECRET_KEY
   unset TWITTER_ACCESS_TOKEN
   unset TWITTER_ACCESS_SECRET
```

Add `export` at the bottom of activate file for each variable.

```
export TWITTER_API_KEY={enter_your_key}
export TWITTER_API_SECRET_KEY={enter_your_key}
export TWITTER_ACCESS_TOKEN={enter_your_key}
export TWITTER_ACCESS_SECRET={enter_your_key}
```

Activate your virtual environment

    source env/bin/activate

Now your are ready to work in python. Fist thing I like to do is create a file called settings.py in the root folder of my project and then import the environment variables there so I can reference them elsewhere in the project easily:

```py
import os

consumer_key = os.environ[“TWITTER_API_KEY”]
consumer_secret = os.environ[“TWITTER_API_SECRET_KEY”]
access_token = os.environ[“TWITTER_ACCESS_TOKEN”]
access_token_secret = os.environ[“TWITTER_ACCESS_SECRET”]
```

## Python time!

    print('Hello World!')
    ...
