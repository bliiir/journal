* [Installing Python 3 on Mac OS X](https://docs.python-guide.org/starting/install3/osx/#install3-osx)
* [Use Python Effectively on OS X](http://blog.manbolo.com/2014/09/27/use-python-effectively-on-os-x)


## Brew

### Install homebrew
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### Install Zsh shell
    brew install zsh

    # Install Oh My Zsh
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

    # Set python path in `~/.profile` to use python3 as the default
    export PATH="/usr/local/opt/python/libexec/bin:$PATH"

    # Install python
    brew install python

    # Set path
    brew install git


## Pip
Homebrew installs pip into the Homebrew Pythons directory.

    # virtualenv
    pip3 install virtualenv

    # virtualenvwrapper
    pip3 install virtualenvwrapper
