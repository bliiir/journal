*journal*
Rasmus Groth
*20181024, Barcelona, Spain*

# .gitignore template
Sources: [1](https://github.com/gboeing/osmnx/blob/master/.gitignore)

```
# secrets #
###########
*.pem

# Python related apps and frameworks #
######################################

# Django stuff:
local_settings.py

# Flask stuff:
instance/
.webassets-cache

# Scrapy stuff:
.scrapy

# Sphinx documentation
docs/_build/

# PyBuilder
target/

# celery beat schedule file
celerybeat-schedule

# Spyder project settings
.spyderproject

# Rope project settings
.ropeproject

# PyCharm IDE idea files
.idea

# Python virtual environment #
##############################
env/
ENV/
venv/
.env
.python-version

# Pip Installer logs #
######################
pip-log.txt
pip-delete-this-directory.txt

# Byte-compiled / optimized / DLL files #
#########################################
__pycache__/
*.py[cod]
*$py.class

# Distribution / packaging #
############################
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
*.egg-info/
.installed.cfg
*.egg

# PyInstaller #
###############
#  Usually these files are written by a python script from a template
#  before PyInstaller builds the exe, so as to inject date/other infos into it.
*.manifest
*.spec

# Jupyter / IPython Notebook #
####################
.ipynb_checkpoints

# project-setting files #
#########################
*.sublime-project
*.sublime-workspace
.idea

# Unit test / coverage reports #
################################
htmlcov/
.tox/
.coverage
.coverage.*
.cache
nosetests.xml
coverage.xml
*,cover
.hypothesis/

# Temp files #
##############
.temp
.pytest_cache

# Shell #
#########
tests/run_tests.bat

# Databases #
#############
*.sql
*.sqlite
*.sqlite3

# Logs #
########
*.log

# Translations #
################
*.mo
*.pot

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Compiled source #
###################
*.com
*.class
*.dll
*.exe
*.o
*.so
*.pyc
*.pyo

# Editor generated files #
##########################
*.swp
*.swo
*~

# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```
