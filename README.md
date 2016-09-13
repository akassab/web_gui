CKWatson Online
===============

A Chemical Kinetics Simulator Game as a webapp, written in Python.

Installation
------------

###Install Python3 from [Official Website][].

Warning: Do not use `brew`, `pyenv` or `virtualenv`, since they will create a non-framework environment of Python, which is required by the `Matplotlib`. I know this pollutes the system environment, but sorry :(

[Official Website]: https://www.python.org/downloads/

####Append binary file directory of Pyhton3 to your PATH variable

This allows auto detection of Python3 binaries.

    $ echo 'export PATH=$PATH:/Library/Frameworks/Python.framework/Versions/3.5/bin' >> ~/.bashrc 

###Install requirements:

    $ pip3 install -r requirements.txt
    $ brew install redis

the second line of which requires [Homebrew](http://brew.sh/). More info about Redis can be found [here](http://redis.io/).


Run the server
--------------

### Run locally

#### The complete method
In one terminal, do:

    $ redis-server

Then, in another terminal:

    $ sudo /Library/Frameworks/Python.framework/Versions/3.5/bin/gunicorn run:app --worker-class gevent --bind 127.0.0.1:80 --reload --timeout 6000

#### The short method
_Alternatively_, you can run the boot script directly:

    $ sudo run.py

This uses Flask itself to host the server, but would lose the ability to send [Server-Sent Events](https://github.com/singingwolfboy/flask-sse).

### Run on Heroku 

Please note that GitHub Auto-Deployment on Heroku does not support `git submodules`, so we have to do it manually.

Heroku does not support `git submodules` unless they are specified with a URL using a `git://` protocol. Therefore, to push a commit to the Heroku server, one has to use this command:

    perl -pi -e 's/url = https/url = git/g' .gitmodules && git push heroku && perl -pi -e 's/url = https/url = git/g' .gitmodules

We have to do the double `perl` call every time we want to push to Heroku, since GitHub needs `https://` protocol for writing access.

Folder Structure
----------------

- `ckwatson` is where the actual code are stored.
- `Puzzle` is the repository of puzzle definitions. Admin can add puzzles there using the `create` page.
- `results` stores the computed results as well as plotted figures. Not really human-readable.