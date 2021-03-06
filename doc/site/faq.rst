template: doc.html
title: FAQ

FAQ
===

What is a slow client?
  A slow client is defined as a request that can take an arbitrary amount of
  time to send or read a request. Sometimes due to network performance or
  because it is a malicious client attempting to cause problems. Check out
  the slowloris_ script to generate slow client traffic.

What is a fast client?
  Generally speaking a fast client is something that is being served over the
  local network or from the same machine. This generally would refer to requests
  forwarded from an upstream proxy. Also see the above FAQ for what a fast
  client is not.
 
Why only fast clients?
  By designing a web server to only handle fast clients we can greatly simplify
  the implementation. Think of it as a separation of concerns where your proxy
  handles talking to the big bad world of the internet and filters the requests
  to your application code.

How might I test a proxy configuration?
  Check out slowloris_ for a script that will generate significant slow
  traffic. If your application remains responsive through out that test you
  should be comfortable that all is well with your configuration.

How do I reload my application in Gunicorn?
  You can gracefully reload by sending HUP signal to gunicorn::

    $ kill -HUP masterpid


How do I increase or decrease the number of running workers dynamically?
    To increase the worker count by one::

        $ kill -TTIN $masterpid
    
    To decrease the worker count by one::

        $ kill -TTOU $masterpid

  
How do I set SCRIPT_NAME?
    By default ``SCRIPT_NAME`` is an empy string. The value could be set by
    setting ``SCRIPT_NAME`` in the environment or as an HTTP header.

How to name processes?
    You need to install the Python package setproctitle_. Then you can name
    your process with `-n` or just let the default. If you use a configuration
    file you can set the process name with the proc_name option.

.. _slowloris: http://ha.ckers.org/slowloris/
.. _setproctitle: http://pypi.python.org/pypi/setproctitle