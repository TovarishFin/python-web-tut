# personal notes

## important general python take aways

1. setup virtual environment to keep deps from being global
  * env easiest to just put in project directory... can include in git...
  * `python -m venv venv`
    * last venv is just name of env you want to setup...
  * `source venv/bin/activate`
    * puts you in virtual env
    * `deactivate` takes you out

1. if going to make installable, should start with that first
  * add a `setup.py` (see bottom for example)
  * add a `MANIFEST.in` have static files that need to be copied over
1. install project while in venv in dir using `pip install -e .s`
  * will look for `setup.py`

1. python has a built sqlite
1. pytest and coverage are the common ways of covering both subjects their names imply...
  * (pytest)[https://pytest.readthedocs.io/en/latest/]
  * (coverage)[https://coverage.readthedocs.io/en/coverage-4.5.1/]
1. I really need to spend more time getting to know how testing works...
1. production should be served through something else such as [waitress](https://docs.pylonsproject.org/projects/waitress/en/latest/)

## some examples

### `setup.py`
```
from setuptools import find_packages, setup

setup(
    name='flaskr',
    version='1.0.0',
    packages=find_packages(),
    include_package_data=True,
    zip_safe=False,
    install_requires=[
        'flask',
    ],
)
```
packages tells Python what package directories (and the Python files they contain) to include. find_packages() finds these directories automatically so you don’t have to type them out. To include other files, such as the static and templates directories, include_package_data is set. Python needs another file named MANIFEST.in to tell what this other data is.

### `MANIFEST.in`
```
include flaskr/schema.sql
graft flaskr/static
graft flaskr/templates
global-exclude *.pyc
```
This tells Python to copy everything in the static and templates directories, and the schema.sql file, but to exclude all bytecode files.
