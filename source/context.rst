Introduction
************

There are a few things we need to explain before getting stuck in.

We focus on the overall picture. To do this we use a few analogies not to be
taken too literally.

The Internet
============

The internet is a network of computers. Its goal is to enable communication
between them.

Your family, friends, colleagues, and acquaintances can be thought of as 
a network of people. (This is how social networks model our relationships.)

To communicate we must have a means by which our messages reach the intended
destination.

On the one hand we need something physical to connect the computers. These are
the wires.

On the other hand we need some conventions (software) to ensure messages reach their
destinations.

One way this is done over the internet is called TCP/IP.

TCP ensures the messages arrive safely with nothing missing.
Every computer has an IP which is a unique address.

You can think of TCP as an envelope and IP as the address on it.

Http and the Request / Response cycle
=====================================

To communicate effectively the elements of a network need to agree on some
protocol. That protocol for humans can be english. Other protocols exist.

Computers on the internet use Http to communicate.

Every time you click on a link, or type a url and enter into a browser, you are
making what is called an http GET request.

Here is an example that uses curl from the command line as a client::

    $ curl -sv www.example.com -o /dev/null
    * About to connect() to www.example.com port 80 (#0)
    *   Trying 93.184.216.119...
    * Connected to www.example.com (93.184.216.119) port 80 (#0)
    > GET / HTTP/1.1
    > User-Agent: curl/7.30.0
    > Host: www.example.com
    > Accept: */*
    >
    < HTTP/1.1 200 OK
    < Accept-Ranges: bytes
    < Cache-Control: max-age=604800
    < Content-Type: text/html
    < Date: Thu, 21 Aug 2014 12:09:46 GMT
    < Etag: "359670651"
    < Expires: Thu, 28 Aug 2014 12:09:46 GMT
    < Last-Modified: Fri, 09 Aug 2013 23:54:35 GMT
    < Server: ECS (iad/182A)
    < Content-Length: 1270
    <
    < <!doctype html>
    < <html>
    < <head>
    <     <title>Example Domain</title>
    < </head>
    < <body>
    < <div>
    <     <h1>Example Domain</h1>
    <     <p>This domain is established to be used for illustrative examples in documents.</p> 
    < </div>
    < </body>
    < </html>

Note this has been abridged.

The lines starting with:

- '*' is information from the curl program.
- '>' is the http request text that curl is sending.
- '<' is the http response text that curl received.

Note that the response includes the html page that will be rendered in
a browser.

Tip:

    Http is just text. We send text requests, we recieve text responses. All
    complex pretty pages in the browser are created from these text responses.

The Client Server Architecture
==============================

In software development an architecture is a way of organising code you see time and time
again. Its also called a pattern. Similar perhaps to how journalists follow
a pattern when structuring their articles.

Think about the meaning of the words.

A browser is a great example of a client. It sends http requests to a server.
A server returns an http response, which the browser then renders as a web page.

We will see other examples of a client - server architecture when we introduce
using databases.

HTML
====

Browsers understand how to render HTML.

HTML is a way to structure text.

.. code-block:: html

    <!doctype html>
    <html>
    <head>
        <title>Example Domain</title>
    </head>
    <body>
    <div>
        <h1>A Header</h1>
        <p>Here is some text between p elements</p> 
    </div>
    </body>
    </html>

Note it consists of elements like this: `<el>content<\el>`

We won't delve any deeper than this as we don't need to.

Databases
=========

Data, or information, needs to be stored somewhere.

Typically we save data in files.

Databases are another way of saving data which has some advantages over plain
files.

Web applications often save data in databases rather than files.

You can think of a database much as you would spreadsheet software. It stores
information in a collection of tables.


Exercise
========

Using Chrome, open developer tools: view/Developer/DeveloperTools

.. image:: /images/open-dev-tools-chrome.png

A tab will pop up. Click on the Network tab.

Now type a URL (web address) that is familiar to you.

Inspect the http GET request.

Here we try with `www.example.com`:

.. image:: /images/req-res-chrome.png

Note we have same information we found with `curl` above. It is presented in
a more user friendly way however.

Explore one of your favourite websites using the developer tools to inspect
what is going on at the http network level.

Take Away
=========

All internet experiences, online shopping, news, videos, sending texts... boil down to
computers sending messages much like what we have described above.

Http is not the only protocol in town, but the concept of computers acting as 
clients and servers communicating by sending requests and responses is almost
universal.
