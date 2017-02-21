.. _installation_ubuntu:

Installation on Ubuntu and Debian
#################################

The following Installation manual describes the neccessary steps on a recent Ubuntu or Debian system. We assume that Apache 2.4 is running on the system. Notes on `PHP 7 <installation_ubuntu.html#php-7>`_  and `Apache 2.2  <installation_ubuntu.html#instructions-for-apache-2-2>`_ are added below. This example uses PostgreSQL as database system.

Please take note of the `system requirements <systemrequirements.html>`_, where you can also find the Download links to Mapbender3.

There are also the neccessary components listed that you can install like this:

.. code-block:: bash

  sudo apt-get install php5 php5-pgsql php5-gd php5-curl php5-cli php5-sqlite sqlite php-apc php5-intl curl openssl


Additionally for development:
 
.. code-block:: bash

 apt-get install php5-bz2


Load the Apache rewrite-module:

.. code-block:: bash

  sudo a2enmod rewrite

Configure the Apache Alias. We assume that Mapbender3 is unzipped into **/var/www/mapbender3** (see the `System Requirements and Download <systemrequirements.html#download-of-mapbender3>`_ chapter for details). You can easily unpack Mapbender3 to a different directory and only adjust the following file to refer to the right directory.

Create the file **/etc/apache2/sites-available/mapbender3.conf** with the content below. 

.. code-block:: apache

 Alias /mapbender3 /var/www/mapbender3/web/
 <Directory /var/www/mapbender3/web/>
  Options MultiViews FollowSymLinks
  DirectoryIndex app.php
  Require all granted
   
  RewriteEngine On
  RewriteBase /mapbender3/
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteRule ^(.*)$ app.php [QSA,L]
 </Directory>

Aktivieren Sie danch die Seite mit

.. code-block:: bash
                
   a2ensite mapbender3.conf

Reload your Apache server.

.. code-block:: bash

 service apache2 reload


PHP 7
-----
 
PHP 7 needs additional packages. The list of packages for PHP 7:

.. code-block:: bash

  sudo apt-get install apache2 libapache2-mod-php php php-pgsql php-gd php-curl php-cli php-xml php-sqlite3 sqlite3 php-apcu php-intl openssl php-zip php-mbstring php-bz2
  

Enable PHP 7 in Apache

.. code-block:: bash

  a2enmod php7.0


Instructions for Apache 2.2
---------------------------

Some versions of Debian support for Apache 2.2 to drop the mapbender3.conf file into the directory ``/etc/apache2/sites-available`` and the activation with the command ``a2ensite``. Depending on the operating-system the file has to be placed into the directory ``/etc/apache2/conf.d/``.

Activate the Rewrite-Modul of Apache.

.. code-block:: bash

 sudo a2enmod rewrite

Unlike version 2.4, Apache 2.2 uses other directives and other default values (``Order`` and ``Allow``, ``AllowOverride``) that has to be written into the mapbender3.conf file. These differences are explained in the `Upgrade-Guide from Apache 2.2 to Apache 2.4 <http://httpd.apache.org/docs/2.4/upgrading.html>`_.

Apache 2.2 configuration ``mapbender3.conf``:

.. code-block:: apache

  ALIAS /mapbender3 /var/www/mapbender3/web/
  <Directory /var/www/mapbender3/web/>
    Options MultiViews FollowSymLinks
    DirectoryIndex app.php
    AllowOverride none
    Order allow,deny
    Allow from all
    
    RewriteEngine On
    RewriteBase /mapbender3/
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^(.*)$ app.php [QSA,L]
 </Directory>

 
Check
-----

Check that the Alias is working:

* http://localhost/mapbender3/

Open Symfony´s Welcome Script config.php. This script checks whether all necessary components are installed and configurations are done. If there are still problems, you should fix them.
 
* http://localhost/mapbender3/config.php


.. image:: ../../../figures/mapbender3_symfony_check_configphp.jpg
     :scale: 80 


Configuration of Mapbender3 
---------------------------

Set the write permission for user (u), group (g) and others (a) and rights. Assign the files to the Apache user (www-data).

.. code-block:: bash

 sudo chmod -R ugo+r /var/www/mapbender3
 sudo chown -R www-data:www-data /var/www/mapbender3
 sudo chmod -R ug+w /var/www/mapbender3/web/uploads


Adapt the Mapbender3 configuration file parameters.yml (app/config/parameters.yml) and define the database you want to create. Further information is available in the chapter `Configuring the database <../database.html>`_.

.. code-block:: yaml

    database_driver:   pdo_pgsql
    database_host:     localhost
    database_port:     5432
    database_name:     mapbender3
    database_path:     ~
    database_user:     postgres
    database_password: secret
 
Run the app/console commands. You find detailed information for this commands in the chapter `Details of the configuration of Mapbender3 <configuration.html>`_.

.. code-block:: bash

 cd /var/www/mapbender3
 app/console doctrine:database:create
 app/console doctrine:schema:create
 app/console assets:install web
 app/console fom:user:resetroot
 app/console doctrine:fixtures:load --fixtures=./mapbender/src/Mapbender/CoreBundle/DataFixtures/ORM/Epsg/ --append
 app/console doctrine:fixtures:load --fixtures=./mapbender/src/Mapbender/CoreBundle/DataFixtures/ORM/Application/ --append

Installation of Mapbender3 is done. 

Check the config.php again:

* http://localhost/mapbender3/config.php

You have to set write permission to app/cache, app/logs and web/uploads.

.. code-block:: bash

 sudo chmod -R ug+w /var/www/mapbender3/app/cache
 sudo chmod -R ug+w /var/www/mapbender3/app/logs
 sudo chmod -R ug+w /var/www/mapbender3/web/uploads


You can start using Mapbender3 now.

* http://localhost/mapbender3/

Click on the Login-link at top-right to get to the login page. Log in with the new user you created. 

You can open the developer mode when you run app_dev.php: http://localhost/mapbender3/app_dev.php

To learn more about Mapbender3 have a look at the `Mapbender3 Quickstart <../quickstart.html>`_.
