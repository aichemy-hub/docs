Diagnosing NOMAD
================

Go through all sections one a time.

Check if you can reach the server
---------------------------------

Enter http://192.160.103.85 into the browser (this link should also be
bookmarked). If you can't reach NOMAD, it may mean that either the server or
proxy is offline. If you can reach http://aichemy-nmr.ch.ic.ac.uk, on a
computer connected to the college network, ie not one of the lab computers,
then the server is running and it's probably the proxy that is offline.

To verify the proxy is working, go on ``serv-10`` and run
``ps aux | grep caddy`` to see if caddy is running. If it is running you should
see something like ``/usr/local/bin caddy run --config /etc/caddy/Caddyfile`` in the output.
If it is not running run:

.. code-block:: bash

  /usr/local/bin/caddy run --config /etc/caddy/Caddyfile &


which will launch it in the background.


Check you are logged in as default user on IconNMR
--------------------------------------------------

If not, log in as the default user.

Check the instrument is connected to the server
-----------------------------------------------

- First, check that the instrument is connected to the server by going to
  the NOMAD UI at http://192.160.103.85 and looking at the instrument list.
  It should say if the instrument is connected or not. If the instrument is connected,
  this is not the issue.
- If the instrument is not connected check if the nomad client is running on the computer.
  Run ``ps aux | grep node`` if the results show something line ``node ./src/app.js run -v``
  then the client is running. If it is not, start it with by running ``nomad-client`` in
  the terminal.
