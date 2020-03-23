# Virtual Environments Cheatsheet

## venv
venv is built into core python

| Command| Description |
| :-- | :-- |
| `pip install --upgrade pip -U` | Upgrade pip to latest verions |
| `python3 -m venv env` | Creates a virtual environment called my_first_env |
| `source env/bin/activate` | Activate the environment you have to `source` the activate file in the bin subfolder of the virtual environment |
| `deactivate` | Leave the venv |
| `pip freeze > requirements.txt` | Create a requirements.txt to store dependencies for the virtual environment in a textfile |
| `pip install -r requirements.txt` | Install the dependencies using the requirements.txt file |


Check out the note on setting environment variables in the [20180925_environment_variables.md](https://github.com/bliiir/journal/blob/master/notes/20180925_environment_variables.md) note


## virtualenv
virtualenv is an installed package

| Command | Effect |
| :-- | :-- |
| `pip install virtualenv` | Install virtual env |
| `virtualenv venv` | Create new virtual environment with the default python interpreter |
| `virtualenv venv --no-site-packages` | Create a new virtual env using only the env packages - no global packages |
| `virtualenv -p /usr/bin/python2.7 venv` | Create a virtualenv using a specific interpreter
| `deactivate` | Deactivate the virtualenvironment
| `rmvirtualenv venv` | Delete the virtual environment |
| `lsvirtualenv` | List all the available environments |
| `virtualenv --relocatable ENV` | Make the virtual environment ENV relocatable |


## virtualenvwrapper
virtualenvwrapper is an installed package

| Command | Effect |
| :-- | :-- |
| `pip install virtualenvwrapper` | Install virtualenvwrapper |
| `source /usr/local/bin/virtualenvwrapper.sh` | Add it to your PATH (`~/.profile` for example) |
| `mkvirtualenv env1` | Make a virtual environment called env1 |
| `workon env1` | Activate virtual environment |
| `workon` | List all virtual environments |
| `rmvirtualenv env1` | delete virtual environment env1 |


## pyenv
https://github.com/pyenv/pyenv/blob/master/COMMANDS.md
https://github.com/pyenv/pyenv-virtualenv
https://saltfishsplash.com/2019/01/pyenv-and-virtualenv-cheatsheet/

`brew install pyenv`
`brew install pyenv-virtualenv`

export PYTHON_CONFIGURE_OPTS="--enable-framework"

| Command | Effect |
| :-- | :-- |
| `pyenv install --list` | List all versions available for install using pyenv |
| `pyenv install <python version>` | Installs <python version> as pyenv |
| `pyenv versions` | List all installed pyenv Python versions |
| `pyenv global` | Show the global Python version |
| `pyenv local` | Show the local Python version |
| `pyenv local <version>` | Set the local Python version |
| `pyenv global <version>` | Set the global Python version |
| **Virtual Environments** | |
| `pyenv virtualenv <python_version> <virtual_environment_name>` | Create a new virtual environment with the indicated python version |
| `pyenv virtualenvs` | List virtual environments |
| `pyenv activate <name>` | Activate the pyenv-virtual environment installed with pyenv  |
| `pyenv deactivate` | Deactivate the current pyenv-virtualenv  |
| `pyenv uninstall <my-virtual-env>` | Uninstall/delete the pyenv-virtualenv my-virtual-env |
| `pyenv virtualenv-delete my-virtual-env` |  Uninstall/delete the pyenv-virtualenv my-virtual-env |


## Links

[What is the difference between venv, pyvenv, pyenv, virtualenv, virtualenvwrapper, pipenv, etc?](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)
