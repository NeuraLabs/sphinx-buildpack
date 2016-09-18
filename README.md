Golden Sphinx Buildpack
=======================

This is a [Heroku Buildpack](https://devcenter.heroku.com/articles/buildpacks) for building and serving a site using Sphinx.

Using this buildpack will override whatever `Procfile` your repo has and will instead use [goldensphinx](https://github.com/yoavram/goldensphinx) to build and serve a Sphinx documentation site. Refer to [goldensphinx](https://github.com/yoavram/goldensphinx) docs for a list of environment variables you can set to configure how Sphinx builds the docs and how gunicorn serves them.

Usage
-----

This is a usage example for working with [dokku]().

First, on the dokku server:

```sh
user@host:~$ dokku apps:create <app_name>
Creating cassandra_docs... done
user@host:~$ dokku config:set <app_name> BUILDPACK_URL=https://github.com/NeuraLabs/sphinx-buildpack.git
-----> Setting config vars
       BUILDPACK_URL: https://github.com/NeuraLabs/sphinx-buildpack.git
-----> Restarting app <app_name>
App <app_name> has not been deployed
```

Then, on your machine in the repo folder:

```sh
user@local  ~/path/to/repo $ git remote add docs user@host:<app_name>
user@local  ~/path/to/repo $ git push docs master
```

Installing dependencies
-----------------------

The buildpack is based on [Conda](http://conda.pydata.org/), the Python distribution for scientific computing by Continuum Analytics.

To control what binary packages are installed by conda, supply a
`conda-requirements.txt` file (which can be created by capturing the output
of `conda list -e` for your working conda environment).
Like when using the standard buildpack for python from Heroku, you can also
still supply a `requirements.txt` file for [pip](https://github.com/pypa/pip)
to process.  In this way, you can install binary packages via conda for
everything you can and still use pip for anything you can't.
