.. _toctree-directive:

Testing and debugging the Labmanager
====================================

Here we present details on how to debug new developments of the LabManager. First, we briefly present  the way  how to install the Labmanager for development purposes, followed by an explanation on how Eclipse IDE can be used to debug Labmanager.

Labmanager quick installation for testing
-----------------------------------------

This document explains how to install the Labmanager from scratch over a Ubuntu 12.04 machine. The steps are the following:

1. Dependencies installation::

    sudo apt-get install build-essential

    sudo apt-get install libmysqlclient-dev

    sudo apt-get install libsasl2-dev libldap2-dev

    sudo apt-get install libxml2-dev libxslt1-dev

    sudo apt-get install libfreetype6-dev libpng12-dev

    sudo apt-get install build-essential python-dev

    sudo apt-get install mysql-server

2. Download the code from git::

    git clone https://github.com/gateway4labs/labmanager

3. Install and upgrade requirements::

    cd labmanager

    pip install -r requirements.txt

    pip install --upgrade -r requirements.txt


4. Create the configuration file, based on the config.py.dist file that comes with the source code::

    cp config.py.dist config.py

5. Open config.py with your favourite text editor and include the following information, replacing the words in CAPITALS with your information::

    env_config = {'engine' : 'mysql', 'username' : 'YOUR_USERNAME', 'password' : 'YOUR_PASSWORD', 'dbname' : 'YOUR_DB_NAME', 'host' : 'localhost', 'pymysql' : True}

6. Deploy the application (e.g. create the database, ...)::

    python deploy.py -cdu

7. Run the application in development mode::

    python run.py

Debugging with Eclipse
----------------------

By following the previous steps the application is running with the built-in Python debugger enabled, which reloads the application when it detects changes in the code. If you plan to debug the application using an external debugger (e.g. PyDev on Eclipse IDE), for instance, because you want to be able to perform step by step executions, you have to follow these steps:

1. Install Eclipse IDE::

    sudo apt-get install eclipse

2. Install Pydev (Python plugin for Eclipse):

    Follow the installation guide `here <http://pydev.org/manual_101_install.html>`_.

3. Make your Eclipse work with virtualenv (full instructions in Spanish `here <http://www.cuble.es/integrar-virtualenv-con-eclipse-pydev>`_). NOTE: This assumes your are working in a virtualenv, skip this point otherwise.

	a. Once you have a Eclipse project created based on PyDev, right-click on the project and select "Properties".

	b. In the "PyDev – Interpreter/Grammar" entry, you will see the following window:

	.. image:: /_static/eclipse-virtualenv-1.png
 
	c. Click on "Click here to configure an interpreter not listed". Then we see the window shown in the following figure:

	.. image:: /_static/eclipse-virtualenv-2.png
 

	d. Click on "New". Then, we have to include the route to the Python executable in the virtualenv of interest. 

	e. After clicking "Ok", Eclipse will  scan the route looking for libraries, and will offer the possibility to  add more libraries. In this point, we will have to add "/usr/lib/python2.7" (or the Python version we have installed in our computer), as can be seen in this figure.

	.. image:: /_static/eclipse-virtualenv-4.png
 
 	f. Click "Ok" several times until you get back to the first figure presented in this document. In this window, select the newly created interpreter and click "Ok".


4. Open the config.py file in the labmanager installation and set::

    DEBUG = False 

5. Once you save the change to the config.py you are ready to debug your installation of LabManager, using breakpoints, watching variables, ...


