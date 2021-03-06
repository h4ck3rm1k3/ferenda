Misc notes on how ferenda is developed
======================================

Release process
---------------

Prep for release by creating a release branch off master

$ git branch
* master
$ git checkout -b release/0.1.0
# update ferenda/__init__.py, CHANGELOG.md, run last minute tests (in particularly, run "tox" if setup.py has changed) and generally tinker around
$ git commit -a -m "Final release prep"
$ git tag -a "v0.1.0" -m "Initial release"
$ git push orgin release/0.1.0
$ git push --tags # makes the release show up in Github
$ python setup.py register
$ python setup.py sdist upload
$ git checkout master
$ git merge release/0.1.0
# update ferenda/__init__.py to eg version=0.1.1-dev
$ git commit -m "start of next iteration" ferenda/__init__.py
$ git push


Also, you should update readthedocs to feature the new point relase as
the built one. Note that you might need to re-build 'latest' on RTD
before the new tag shows up under Versions there.

Smoke-testing the released code
-------------------------------

In a new virtualenv:

$ pip install --extra-index-url https://testpypi.python.org/pypi ferenda

