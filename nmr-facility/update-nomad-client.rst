To update the NOMAD client software, we need to download the new `.zip` file from GitHub, replace the existing code with it, then restart the client.

The process is similar to the process for installing the NOMAD client(https://github.com/aichemy-hub/docs/blob/master/nmr-facility/installing-nomad-client.rst), but shorter. 

First, we need use port forwarding to access the internet.

Create an internet connection by creating an SSH
tunnel to ``serv-10`` through which we can gain temporary internet
access.

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
* Download "Source code (zip)" of the latest version or version you want

Next, we need to stop the existing client.

* This may be in an open Konsole window, so close any windows that are running ``nomad-client`` or similar. 
* It may also be running in the background so type ``ps`` to get the PIDs of any processes running ``nomad-client`` or any node or npm commands. 
* Type ``kill -9 <PID>`` replacing <PID> with the actual PID.

Now we can remove the old version of the code.
**Double check the next command before pressing enter. Typing "sudo rm -rf" the wrong directory can be catastrophic.**
The ``rm -rf`` flag means "recursively and forcibly remove a directory" (No recycle bin or second chances!) 
Go to /opt/ in the terminal and CAREFULLY type ``sudo rm -rf nomad-spect-client`` to remove the directory entirely.

Next put the new code in its place: 

* Go to you Downloads folder and extract the new zip file:
  ``unzip nomad-spect-client-3.5.5.zip``
* Move the extracted folder:
  ``sudo mv nomad-spect-client-3.5.0 /opt/nomad-spect-client``

In the new directory you've just created in ``/opt/nomad-spect-client`` run ``npm install`` to update the node dependencies.

Next, we need to recreate the status_files and submit_files directories:

.. code-block:: bash

  mkdir status_files
  mkdir submit_files

Now we can reconfigure the updated version of the client:

.. code-block:: bash

  npm run config

Follow the prompts as described at https://www.nomad-nmr.uk/docs/getting-started/client-installation/#config. Ensure you enter the correct instrument ID from http://aichemy-nmr.ch.ic.ac.uk/admin/instruments.

TODO: reconfigure IcoNMR. 

                                                                        

