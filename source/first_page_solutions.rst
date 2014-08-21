Solutions to Creating Web Services
**********************************

`website/urls.py`
=================

.. code-block:: python

    from django.conf.urls import patterns, include, url

    from django.contrib import admin
    admin.autodiscover()

    urlpatterns = patterns('',
        url(r'^$', 'blog.views.hello'),
        url(r'^time$', 'blog.views.time'),
        url(r'^whoami/$', 'blog.views.whoami'),
        url(r'^bmi/$', 'blog.views.bmi'),
        url(r'^admin/', include(admin.site.urls)),
    )

`blog/views.py`
===============

.. code-block:: python

    from django.shortcuts import render

    from django.http import HttpResponse


    def hello(request):
        return HttpResponse('hello there')


    import datetime
    def time(request):
        now = datetime.datetime.now()
        return HttpResponse(now)


    def whoami(request):

        sex = request.GET['sex']
        name = request.GET['name']

        response = 'You are {}, of sex {}'.format(name, sex)

        return HttpResponse(response)

    bmi_html = """
    <html>
    <head></head>
    <body>
        <h1>BMI calculator</h1>
        <p>Your bmi is {}</p>
        <p>see where you are on this chart:</p>
        <img src="http://upload.wikimedia.org/wikipedia/commons/e/e9/Body_mass_index_chart.svg">
    </body>
    </html>
    """

    def bmi(request):

        mass = request.GET['mass']
        height = request.GET['height']

        bmi = float(mass) / float(height)**2

        response = bmi_html.format(bmi)

        return HttpResponse(response)
