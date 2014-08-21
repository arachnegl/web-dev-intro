Creating Web Services
*********************

We will start by programming the server to return a responses to an http GET
request.

We will always need to do two things:

- map a url to a view function
- define the view function 

Saying hello
============

Django provides us with what it calls view functions.

These are orgindary pythong functions, but they take a request object and they
response with a string or what is called an `HTTPResponse` object.

In your blog app, open the `views.py` file.

Add this to it::

    from django.http import HttpResponse

    def hello(request):
        return HttpResponse('hello')

Now we need to configure our website with which request will trigger this view
function. We do this by adding a line to `website/urls.py`::

    urlpatterns = patterns('',
        url(r'^$', 'blog.views.hello_world'),
        url(r'^admin/', include(admin.site.urls)),
    )

In our browser, `http://localhost:8000` responds with 'hello'.

We have responded to a GET request.

We will often follow this pattern of creating a view function and hooking it up to a url.

GET parameters
==============

http GET requests can pass parameters in the URL.

Here is an example::

    http://localhost:8000/whoami/?name=greg&sex=male

The parameter section is defined by ? followed by & separated keys and values.

Here we have the parameters:
- name, equal to greg
- sex, equal to male

As usual we need to do two things create a view function and hook it up in `website/urls.py`

First the view function::

    def whoami(request):

        sex = request.GET['sex']
        name = request.GET['name']

        response = 'You are ' + name + ' and of sex ' + sex

        return HttpResponse(response)

Note that we can extract anything passed in the url after the `?` character
using the request.GET dictionary. 

Now `website/urls.py`::

    urlpatterns = patterns('',
        url(r'^$', 'blog.views.hello'),
        url(r'^time$', 'blog.views.time'),
        url(r'^whoami/$', 'blog.views.whoami'),
        url(r'^admin/', include(admin.site.urls)),
    )

You should now get as a response: `You are greg and of sex male`

Exercises
=========

A clock service
---------------

You can get an exact time by doing the following::
    
    >>> import datetime
    >>> datetime.datetime.now()

Program your server to response the time when it recieves an http GET request
to this url::

    http://localhost:8000/time

You will need to create a view function in `blog/views.py`, and hook it up to a url in
`website/urls.py`.


Body Mass Index Service
-----------------------

You have just been contracted by the NHS to provide a service that calculates
the BMI. Both other websites and mobile apps will be using your service.

The endpoint (url) will respond successfully to the following type of url::

    bmi/?mass_kg=75&heigh=182

Look up the BMI equation on wikipedia, and write a bmi view function and hook
it up to the website urls.

You may have to revisit the notion of type in Python. Remember there is
a difference between `'5'` and `5`.

To transform a number as a string into a number you can cast it using either
int() or float()::
    
    >>> float('5')
    5.0
    >>> int('5')
    5

Your Serivce
------------

By now you have discovered that you can trigger any type of programming sending
ba GET request to your server. You simply hook up a url to a view function.

Come up with something that is useful to you!

Anything that involves simple maths is easily explored.

Solutions:

    You can find some suggestions by adding _solutions to the above url.

