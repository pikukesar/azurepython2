# azurepython2
testing new test
this is a test for recording



You can watch this [YouTube Walkthrough of this process](https://youtu.be/wn59BHutCQA)

#Git clone
![Git clone](https://github.com/pikukesar/azurepython2/blob/3e7997e89ea3257fe34338e561cf4d01e6fcde66/Demo%201-Screen%20Shot%20Git%20clone.png)

#make all Test Passed
![make all Test Passed](https://github.com/pikukesar/azurepython2/blob/3e7997e89ea3257fe34338e561cf4d01e6fcde66/Demo%201%20Make%20all%20passed.png)

#Git Commit and Git Push
![Git Commit and Git Push](https://github.com/pikukesar/azurepython2/blob/3e7997e89ea3257fe34338e561cf4d01e6fcde66/Demo1%20Git%20commit%20and%20Push.png)

#Github Actions Build
![Github Actions](https://github.com/pikukesar/azurepython2/blob/46e09792790aff6415daaaf8e376a285b923c9bd/Git%20Action%20build.png)


[![Python application test with Github Actions](https://github.com/pikukesar/azurepython2/actions/workflows/main.yml/badge.svg)](https://github.com/pikukesar/azurepython2/actions/workflows/main.yml)

# Project Overview . 
This project shows 



## Steps to run this project

* Create a Github Repo (if not created)
* Open Azure Cloud Shell
* Create ssh-keys in Azure Cloud Shell
* Upload ssh-keys to Github
* Create scaffolding for project (if not created)
  - Makefile

Should look similar to the file below

```bash
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

test:
	python -m pytest -vv test_hello.py


lint:
	pylint --disable=R,C hello.py

all: install lint test
```

  - requirements.txt
  
The requirements.txt should include:

```bash
pylint
pytest
```

* Create a python virtual environment and source it if not created

```bash
python3 -m venv ~/.myrepo
source ~/.myrepo/bin/activate
```

* Create initial `hello.py` and `test_hello.py`

hello.py
```python
def toyou(x):
    return "hi %s" % x


def add(x):
    return x + 1


def subtract(x):
    return x - 1
```

test_hello.py
```python
from hello import toyou, add, subtract


def setup_function(function):
    print("Running Setup: %s" % {function.__name__})
    function.x = 10


def teardown_function(function):
    print("Running Teardown: %s" % {function.__name__})
    del function.x


### Run to see failed test
#def test_hello_add():
#    assert add(test_hello_add.x) == 12

def test_hello_subtract():
    assert subtract(test_hello_subtract.x) == 9

```


* Run `make all` which will install, lint and test code.

* Setup Github Actions in `pythonapp.yml`

```yaml
name: Python application test with Github Actions

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.5
      uses: actions/setup-python@v1
      with:
        python-version: 3.5
    - name: Install dependencies
      run: |
        make install
    - name: Lint with pylint
      run: |
        make lint
    - name: Test with pytest
      run: |
        make test
```
