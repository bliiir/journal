# Environment variables

1. Using the terminal, navigate to the folder you want your code in
2. go to terminal: `python3 -m venv env`
3. Open the “activate” file with text editor, add “unset” of your variable names at the deactivate() module.

```
deactivate () {
   unset TWITTER_API_KEY
   unset TWITTER_API_SECRET_KEY
   unset TWITTER_ACCESS_TOKEN
   unset TWITTER_ACCESS_SECRET
```

4. Add `export` at the bottom of activate file for each variable.

```
export TWITTER_API_KEY={enter_your_key}
export TWITTER_API_SECRET_KEY={enter_your_key}
export TWITTER_ACCESS_TOKEN={enter_your_key}
export TWITTER_ACCESS_SECRET={enter_your_key}
```

5. Import os and reference the variables in your settings.py file

```py
import os

consumer_key = os.environ[“TWITTER_API_KEY”]
consumer_secret = os.environ[“TWITTER_API_SECRET_KEY”]
access_token = os.environ[“TWITTER_ACCESS_TOKEN”]
access_token_secret = os.environ[“TWITTER_ACCESS_SECRET”]
```
