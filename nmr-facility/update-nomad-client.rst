To update the NOMAD client software, we need to download the new `.zip` file from GitHub, replace the existing code with it, then restart the client.

The process is similar to the process for [installing the NOMAD client](https://github.com/aichemy-hub/docs/blob/master/nmr-facility/installing-nomad-client.rst), but shorter. 

First, we need use port forwarding to access the internet.

Create an internet connection by creating an SSH
tunnel to ``serv-10`` through which we can gain temporary internet
access.

To create the tunnel, run:

.. code-block:: bash

  ssh -D 8080 lt912@serv10

Replace ``lt912`` with your own username. You will be asked
for you password. Enter your Imperial password.

At this point you should be logged into ``serv10``. While logged into
``serv10`` you will be able to use its internet traffic. Keep this
terminal open while you want to use the internet. We will need
to open a new terminal window for the following work.

To use Firefox to download the latest version, 
we first need to make sure it can use our SSH tunnel to connect to the internet.
The following settings should be prepopulated from the initial installation/last update
after you select "Manual proxy configuration":

* Open Firefox and go to Settings
* Scroll down to "Network Settings"
* Click on the "Settings..." button
* Select "Manual proxy configuration"
* Under SOCKS Host enter: 127.0.0.1
* For the corresponding port enter: 8080
* Ensure SOCKS v5 is selected
* Ensure Proxy DNS when using SOCKS v5 is selected

Now use Firefox to download the client:

* go to https://github.com/nomad-nmr/nomad-spect-client/releases
* Download "Source code (zip) of the latest version or version you want                                              

                                                                        

