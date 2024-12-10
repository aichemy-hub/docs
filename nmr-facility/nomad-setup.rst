NOMAD Setup
===========

The computers in the lab are disconnected from the college network but are
connected to each other through a local lab network. There is one computer in
the lab ``serv-10`` which is both on the lab network and on the college network
and internet.

The NOMAD system consists of the following components:

* A server (https://github.com/nomad-nmr/nomad-server) running in the college cloud
  available at http://aichemy-nmr.ch.ic.ac.uk.
* A client (https://github.com/nomad-nmr/nomad-spect-client) running on each lab computer
  connected to an NMR machine.

In order for NOMAD to work the client computers must be able to reach the
server via the college network. This is achieved by creating a HTTP proxy on
``serv-10``, via `caddy <https://caddyserver.com/docs>`_. When the client needs
to talk to the NOMAD server, it talks sends an HTTP request to ``serv-10``.
``serv-10`` has caddy running on it (on port 80) and it will send this
request to the server. It will then send the response back to the client. Check
the `debug guide <./nomad-debug-guide.rst>`_ for more information on how to
check the caddy proxy is working properly.

Each client computer has to be running the NOMAD client, found on
https://github.com/nomad-nmr/nomad-spect-client. The NOMAD client is
responsible for getting instructions from the server and writing input files
which iconNMR then executes.

When an NMR experiment is executed, the data will be copied onto the NOMAD
server and available to users on the college network via
http://aichemy-nmr.ch.ic.ac.uk.


Updating the NOMAD server
-------------------------

Note that my username is ``lt912``. You will need to replace this with yours.
To check which versions of NOMAD are available, see the `releases page
<https://github.com/nomad-nmr/nomad-server/releases>`_.

* SSH into the ssh gateway
  (`more details <https://www.imperial.ac.uk/admin-services/ict/self-service/connect-communicate/remote-access/remotely-access-my-college-computer/>`_)

  .. code-block:: bash

    ssh lt912@sshgw.ic.ac.uk

* From the gateway, SSH into the server

  .. code-block:: bash

    ssh aichemy-nmr.ch.ic.ac.uk

* Go into the nomad directory

  .. code-block:: bash

    cd /nomad

* Open the ``docker-compose.yaml`` file

  .. code-block:: bash

    sudo vim docker-compose.yaml

* Change the version number in the following lines to your chosen version

  .. code-block:: yaml

* Restart the server by running

  .. code-block:: bash

    sudo docker compose up -d

* Done! You can close you SSH session.
