Setup
*****

Project folder
==============

Lets create a project directory::

    mkdir website
    cd website

Virtualenv
==========

Its good practice to setup a sandbox python environment.

We create a local safe python environment in our folder.

We create the new python environment with::

    python -m venv website

You activate or deactivate the python environment::

    $ source website/bin/activate   # activates
    $ deactivate                    # deactivates

Installing Django
=================

Pip is a way to install python code. Python code is installed as a package.

To list all currently installed python packages::

    $ pip freeze

To install a Django::

    $ pip install django


Creating Django project
=======================

We use a script supplied by django to set up a new project::
    
    $ django-admin.py startproject website

You should see this folder structure and files generated::

    website
    ├── manage.py
    └── website
        ├── __init__.py
        ├── settings.py
        ├── urls.py
        └── wsgi.py   


The important files are `manage.py`, `settings.py`, and `urls.py`.

settings.py
===========

A lot of configuration is needed to setup a web application.

`website/settings.py` contains a lot of names that define all the configuration
for our website. All the defaults are good for now.

Note the INSTALLED_APPS name is defined as a tuple of strings. We will be
adding to that tuple shortly.

Note also the DATABASES name is defined as a dictionary.

Creating the Database
=====================

Notice that the current directory doesn't include a db.sqlite3 file.

Django like all web frameworks stores its data in a database. Lets create that
database now::

    python manage.py syncdb

You will see some output such as: `Creating table auth_user`

::

    (django) website $ ./manage.py syncdb
    Creating tables ...
    Creating table django_admin_log
    Creating table auth_permission
    Creating table auth_group_permissions
    Creating table auth_group
    Creating table auth_user_groups
    Creating table auth_user_user_permissions
    Creating table auth_user
    Creating table django_content_type
    Creating table django_session

    You just installed Django's auth system, which means you don't have any superusers defined.
    Would you like to create one now? (yes/no): yes
    Username (leave blank to use 'greg'):
    Email address:
    Password:
    Password (again):
    Superuser created successfully.
    Installing custom SQL ...
    Installing indexes ...
    Installed 0 object(s) from 0 fixture(s)

Now the top level folder website contains a file called `db.sqlite3`. This is
your database.

Inspecting the Database
=======================

A database application is like a server.

We send requests using clients. The clients in this case aren't the browser but
typically programs such as our python website.

We will use another server to independently inspect our database.

You launch the client by typing::
    
    sqlite3 db.sqlite3

The `sqlite3` program provides a new type of shell which is meant for
inspecting our database.

Here is an example interaction::

    (django)➜  website  sqlite3 db.sqlite3
    SQLite version 3.7.13 2012-07-17 17:46:21
    Enter ".help" for instructions
    Enter SQL statements terminated with a ";"
    sqlite> .tables
    auth_group                  auth_user_user_permissions
    auth_group_permissions      django_admin_log
    auth_permission             django_content_type
    auth_user                   django_session
    auth_user_groups
    sqlite> select * from auth_user;
    1|pbkdf2_sha256$12000$YqWBCAkWemZC$+hazwa/dPJNczpPitJ2J0KR8UuAX11txLlSkrtAXk5k=|2014-08-21 14:59:05.171913|1|greg||||1|1|2014-08-21 14:59:05.171913
    sqlite>

The `.tables` command lists all the tables that exist in the database. We
recognise these as being the same that were created earlier by running the
`.manage.py syncdb` command.

The  `select * from auth_user;` is SQL. SQL is a language dedicated to programming databases. This command means give me everything in the `auth_user` table.

Type:: 

    sqlite3> .quit

To exit.

Running the server
==================

You run the server with::

    ./manage.py runserver

Now you can send http requests using your browser as client. Enter::
    
    http://127.0.0.:8000/
    
You should see:

.. image:: /images/django-it-worked.png

You can quit the server at any point by pressing together `cntrl + c`
