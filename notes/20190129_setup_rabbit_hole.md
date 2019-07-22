# CCAT pip installs

    pip install --upgrade pip

    pip install psycopg2-binary
    pip install requests
    pip install pgcli

    pip install ccxt
    pip install pandas
    pip install numpy
    pip install sqlalchemy


    brew install python
    brew install jupyterlab

# Jupyter Kernel fuckary

* [Jupyter notebook running kernel in different env](https://stackoverflow.com/questions/37891550/jupyter-notebook-running-kernel-in-different-env)  
* [Execute Python script within Jupyter notebook using a specific virtualenv](https://stackoverflow.com/questions/33496350/execute-python-script-within-jupyter-notebook-using-a-specific-virtualenv)  
* [Use Python Effectively on OS X](http://blog.manbolo.com/2014/09/27/use-python-effectively-on-os-x)
* [Installing Python 3 on Mac OS X](https://docs.python-guide.org/starting/install3/osx/#install3-osx)


## Using Jupyter Notebook with virtual environments
[Using a virtualenv in an IPython notebook](help.pythonanywhere.com/pages/IPythonNotebookVirtualenvs)

Using the virtualenv package

    workon my-virtualenv-name
    pip install tornado
    pip install ipykernel
    python -m ipykernel install --user --name=my-virtualenv-name



# Create a new kernel
    source activate ENVNAME
    pip install ipykernel
    python -m ipykernel install --user --name ENVNAME --display-name "Python (whatever you want to call it)"

Jupyter kernels are located:
/Users/rg/Library/Jupyter/kernels/env


vim /etc/paths


A: Ok - what is my problem?
Q: I can't run the ccat simulation in Jupyter notebooks

Q: Why not?
A: Jupyter notbooks do not use the packages in the virtual environment.

Q: How was is possible to use it before then?
A: I had all the packages installed globally 😳

Q: Did we not work on this before?
A: Yes, we reinstalled Python using the installer instead of the Homebrew installation.

Q: What was wrong with that?
A: I think the notebook was using the virtual environment I had made for the Traktor script which happened to have the right packages.

Q: Hmm, there is something missing here.
A: I know what you mean. Let's walk through it together.

I just fired up jupyter note



Q: Right. That's not good. What are our choices then?
A: Well, we can just not use Jupyter Notebooks at all and instead us
