Install
=======

To run ownCloud, your webserver must have the following installed : ``php5
(>= 5.3), php5-json php-xml php-mbstring php5-zip php5-gdAnd as optional
dependencies: php5-sqlite (>= 3), curl, libcurl3, libcurl3-dev,
php5-curl, php-pdo``

::

    apt-get install apache2 php5 php5-json php-xml php-mbstring php5-zip php5-gd
            apt-get install php5-sqlite curl libcurl3 libcurl3-dev php5-curl php-pdo

You *don’t* need any WebDAV support of your webserver (i.e. apache’s
mod\_webdav) to access your ownCloud data via WebDAV, ownCloud has a
WebDAV server built in.



1. Download
-----------
`Python <http://www.python.org/>`_

Latest 4.0 (4.0.9)
~~~~~~~~~~~~~~~~~~

+ `Download <http://mirrors.owncloud.org/releases/owncloud-4.0.9.tar.bz2/>`_  
+ `MDS <http://mirrors.owncloud.org/releases/owncloud-4.0.9.tar.bz2.md5>`_


Latest 4.5 (4.5.3)
~~~~~~~~~~~~~~~~~~
+ `Download here <http://mirrors.owncloud.org/releases/owncloud-4.5.3.tar.bz2>`_ 
+ `MD5 <http://mirrors.owncloud.org/releases/owncloud-4.5.3.tar.bz2.md5>`_ 
+ `Try the web installer!`_

ownCloud Packages
~~~~~~~~~~~~~~~~~~
`Open Build Service`_

Sync Clients
~~~~~~~~~~~~~~~~~~
`Sync Clients Page`_



2. Install
----------


2.1. Extract ownCloud and copy to your webserver
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``tar -xjf path/to/downloaded/owncloud-x.x.x.tar.bz2``\ ``cp -r owncloud /path/to/your/webserver``

2.2. Set the directory permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The owner of your webserver must own the apps/, data/ and config/
directories in your ownCloud install. You can do this by running the
following command for the apps, data and config
directories:\ ``chown -R www-data:www-data /path/to/your/owncloud/install/data``



Replace ``www-data:www-data`` with the user and group of the owner of your
webserver.



*Note that the data/ directory will only be created after setup has run
(see below) and is not present by default in the tarballs.*

2.3. Enable .htaccess and mod\_rewrite if running apache
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you are running the apache webserver, it is recommended that you
enable ``.htaccess`` files as ownCloud uses them to enhance security and
allows you to use webfinger. To enable .htaccess files you need to
ensure that ``AllowOverride`` is set to ‘All’ in the ``Directory /var/www/``
section of your virtual host file. This is usually in
``/etc/apache2/sites-enabled/000-default``. You should also run ``a2enmod``
``rewrite`` and ``a2enmod headers``. Then restart apache:
``service apache2 restart`` (for Ubuntu systems).In order for the
maximum upload size to be configurable, the .htaccess file in the
owncloud folder needs to be made writable by the server.

2.4. Follow the install wizard
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Open your web browser and navigate to your ownCloud instance. If you are
installing ownCloud on the same machine as you will access the install
wizard from, the url will be:\ ``http://localhost/`` (or
``http://localhost/owncloud``\ For basic installs we recommend SQLite as
it is easy to setup (ownCloud will do it for you). For larger installs
you should use MySQL or PostgreSQL. Click on the Advanced options to
show the configuration options. You may enter admin credentials and let
ownCloud create its own database user, or enter a preconfigured user.


If you are not using apache as the webserver, please set the data
directory to a location *outside* of the document root. See the advanced
install settings.



3. Finished!
------------

Login and start using ownCloud! For more details on configuring your
ownCloud, please visit the `Support Centre`_.


If you plan on using the Webfinger app and your ownCloud installation is
not in the webroot then you’ll have to manually link
``/var/www/.well-known`` to ``/path/to/your/owncloud/.well-known.``



Upgrading
---------

Check the `Upgrade Instructions`_ page.




.. _Try the web installer!: https://download.owncloud.com/download/community/setup-owncloud.php
.. _Open Build Service: http://software.opensuse.org/download/package?project=isv:ownCloud:community&package=owncloud
.. _Sync Clients Page: /sync-clients
.. _Support Centre: /support/
.. _Upgrade Instructions: http://owncloud.org/support/upgrade/