# Virtual environments


| Command| Description |
| :-- | :-- |
| ```python3 -m venv env``` | Creates a virtual environment called my_first_env |
| ```source env/bin/activate``` | Activate the environment you have to ```source``` the activate file in the bin subfolder of the virtual environment |
| ```deactivate``` | Leave the venv |
| ```pip freeze > requirements.txt``` | Create a requirements.txt to store dependencies for the virtual environment in a textfile |
| ```pip install -r requirements.txt``` | Install the dependencies using the requirements.txt file |


Check out the note on setting environment variables in the [20180925_environment_variables.md](https://github.com/bliiir/journal/blob/master/notes/20180925_environment_variables.md) note
