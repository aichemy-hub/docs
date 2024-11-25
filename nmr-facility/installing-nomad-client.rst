To install the NOMAD client on a lab computer we first need to
install Node. To install Node the computer needs to get an internet
connection. We create an internet connection by creating an SSH
tunnel to ``serv-10`` through which we can gain temporary internet
access.

To create the tunnel, run:

.. code-block:: bash

  ssh -D 8080 lt912@serv10

Replace ``lt912`` with your own username. You will be asked
for you password. Enter your Imperial password.

At this point you should be logged into ``serv10``. While logged into
``serv10`` you will be able to use its internet traffic. Keep this
terminal open while you want to use the internet. But we will need
to open a new terminal window for the following work.


Next we want to install node and npm (you will be prompted for the sudo
passsword). First we need to tell yum to use the proxy. Run:

.. code-block:: bash

  sudo vim /etc/yum.conf

Add the following line to the file::

  proxy=socks5h://127.0.0.1:8080


Then run:

.. code-block::

   sudo yum install nodejs npm


Next we need to follow the instructions on
https://www.nomad-nmr.uk/docs/getting-started/client-installation. However,
instead of using git to download the client we will use Firefox. To use Firefox we
first need to make sure it can use our SSH tunnel to connect to the internet:

* Open Firefox and go to Settings
* Scroll down to "Network Settings"
* Click on the "Settings..." button
* Select "Manual proxy configuration"
* Under SOCKS Host enter: 127.0.0.1
* For the corresponding port enter: 8080
* Ensure SOCKS v5 is selected
* Ensure Proxy DNS when using SOCKS v5 is selected

Now use Firefox to download the client:

* go to https://github.com/nomad-nmr/nomad-spect-client
* Click on the big green button called "code"
* Click on "download zip"
* You may want to change which version you download by clickin on the Relases section
  in Github

Now open a new terminal window and:

* go to you Downloads folder and extract the zip you just downloaded:
  ``unzip nomad-spect-client-3.5.0.zip``
* Move the extracted folder (requires sudo password):
  ``sudo mv nomad-spect-client-3.5.0 /opt/nomad-spect-client``

Finally, in the same terminal session make sure you run

.. code-block::

  export https_proxy=socks5h://127.0.0.1:8080

So that npm is able to install things

You can now continue the guide on
https://www.nomad-nmr.uk/docs/getting-started/client-installation.

When the guide asks you to enter the instrument id -- just make sure you've
already added the instrument on the NOMAD server and use that ID.

When prompted for HTTP address of the server while running ``npm run config``, use
``http://192.160.103.85``.

Once config is done make sure you've done all the steps of
https://www.nomad-nmr.uk/docs/getting-started/IconNMR-configuration

Make sure you that you restart icon once youre done configuring it.

To run nomad-client easily make the following file in ``$HOME/bin/nomad-client``.

.. code-block:: bash

  #/usr/bin/env bash

  cd /opt/nomad-spect-client
  npm run verbose &

When the file has been created set it to executable with
``chomd 755 /home/nmrsu/bin/nomad-client``
