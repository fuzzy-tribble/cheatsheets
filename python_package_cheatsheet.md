# Python Package Cheatsheet

This cheatsheet helps me remember setup for python projects (packaged projects specifically)

The final result will be a package published PyPI that can be installed using `pip install mypackage` then `import mypackage` it and use it.

## Setup Workspace
*Note: See pip and venv cheatsheet for more deets*

### Create a venv (work in that only)

```python
# Create venv
python3 -m venv .env

# Activate venv; deactivate venv
source .env/bin/activate
deactivate

# Install packages; save them to reqs file
pip install package
pip freeze > requirements.txt
```

### Create Project Scaffolding / Structure

**Option A: Minimalistic (single installable package)**

```
mypackage/
├── mypackage/
│   ├── __init__.py
│   ├── helloworld.py
│   └── helpers.py
├── tests/
│   ├── helloworld_tests.py
│   └── helpers_tests.py
├── .gitignore
├── LICENSE
├── README.md
├── requirements.txt
└── setup.py
```

*Note: Technically, a package is any group of python modules (*.py files) and an `__init__.py` file (nothing has to be in it...just has to exist). BUT this is the typical minimalist scaffolding that includes a README, LICENSE, etc.*

**Option B: More Realistic Application (app w/ internal packages)**

```python
# Hello World Example
helloworld/
├── bin/
├── docs/
│   ├── hello.md
│   └── world.md
├── helloworld/
│   ├── __init__.py
│   ├── runner.py
│   ├── hello/
│   │   ├── __init__.py
│   │   ├── hello.py
│   │   └── helpers.py
│   └── world/
│       ├── __init__.py
│       ├── helpers.py
│       └── world.py
├── resources/
│   ├── input.csv
│   └── output.xlsx
├── tests/
│   ├── hello
│   │   ├── helpers_tests.py
│   │   └── hello_tests.py
│   └── world/
│       ├── helpers_tests.py
│       └── world_tests.py
├── .gitignore
├── LICENSE
└── README.md
```

```python
# Game Example
mypackage-git
├── LICENSE.md
├──mypackage
│   ├── app.py
│   ├── common
│   │   ├── classproperty.py
│   │   ├── constants.py
│   │   ├── game_enums.py
│   │   └── __init__.py
│   ├── data
│   │   ├── data_loader.py
│   │   ├── game_round_settings.py
│   │   ├── __init__.py
│   │   ├── scoreboard.py
│   │   └── settings.py
│   ├── game
│   │   ├── content_loader.py
│   │   ├── game_item.py
│   │   ├── game_round.py
│   │   ├── __init__.py
│   │   └── timer.py
│   ├── __init__.py
│   ├── __main__.py
│   ├── resources
│   └── tests
│       ├── __init__.py
│       ├── test_game_item.py
│       ├── test_settings.py
│       ├── test_test.py
│       └── test_timer.py
├── pylintrc
├── README.md
└── .gitignore
```

*Note: The toplevel package (mypackage) contains four sub-packages: `common`, `data`, `game`, and `tests` (`resources` is NOT a package, as it doesn't contain an __init__.py).*

***Requirements vs Setup.py:** "pip install" does not look at a requirements.txt, only at install_requires in setup.py. If you're distributing your package via PyPI and `pip install mypackage` should install `foo` and `bar` as dependencies, put them in `setup.py`. If you want to document exactly which packages should be installed for a testing or development venv, put them in `requirements.txt`*

```python
# setup.py
from setuptools import setup

setup(name='funniest',
      version='0.1',
      description='The funniest joke in the world',
      url='http://github.com/storborg/funniest',
      author='Flying Circus',
      author_email='flyingcircus@example.com',
      license='MIT',
      packages=['funniest'],
      zip_safe=False)
```


# Publishing Package on PyPI

```python
# Note: help
$ python setup.py --help-commands

# Register the package (reserve name, upload pkg metadata, create the pipi.python.org webpage)
$ python setup.py register

# Check to see your package website
# http://pypi.python.org/pypi/mypackage/0.1

# First create a source distribution
$ python setup.py sdist

# Test / verify
# Copy the dist/mypackage.tar.gz
# Unpack; install
# Verify it works

# Uploaded file to PyPI
$ python setup.py sdist upload

# Now anyone can run
$ pip install mypackage
```