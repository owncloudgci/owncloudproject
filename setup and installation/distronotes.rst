Distro Notes
============




Archlinux
---------

There are two AUR packages for ownCloud 2:

-  `stable version 3.0`_
-  `development version`_

openSUSE
--------

1. Copy ownCloud to Apache‘s server directory : ``/srv/www/htdocs``
2. Give the web server the necessary permissions:
   ``sudo chown -R wwwrun owncloud``

   -  If you are not a “sudo’er” then you have to become root and
      execute: ``chown -R wwwrun owncloud`` in the directory.
   -  (If you’re using mysql, you have to set the database character set
      to something else then utf-8, for example latin1 otherwise some
      keys will be to long for mysql)

3. Open the folder in a browser and complete the setup wizard

If have followed the steps above and want to try it out, run this
command in a terminal to start Apache if it’s not already running:

1. ``sudo /etc/init.d/apache2 start``
2. Go to `http://127.0.0.1/owncloud/index.php`_ and set it up. Hit the
   enter key to submit the details in the form.

SLES and openSUSE rpm packages build in `ownCloud 2.0.1 openSUSE Build
Service`_

Fedora
------

Make sure SELinux is disabled or else the installation process will fail
with the following message: ``Config file (config/config.php) is not
writable for the webserver`` . Configure Apache:

1. If you already have a website running from Document Root but would
   still like to install OwnCloud you can use a Name-based virtual host
   entry and subdomain.
2. Edit your DNS record following this example: ``point owncloud.foo.com >
   ip.ip.ip.ip``

CENTOS5
-------

1. Create a new file in ``/etc/httpd/conf/`` and call it ``owncloud.conf``.
2. You can use the following as an example:



::

    <IfModule mod_alias.c>
    Alias /owncloud /var/www/owncloud/
    </IfModule>
    <Directory /var/www/owncloud/>
       Options None
       Order allow,deny
       allow from all
    </Directory>
    <VirtualHost *:80>
        ServerAdmin foo@foofarm.com
        DocumentRoot /var/www/html/owncloud
        ServerName owncloud.foo.com
        ErrorLog logs/owncloud.foo.info-error_log
        CustomLog logs/owncloud.foo.info-access_log common

    </VirtualHost>

1. Now edit your httpd.conf file which is usually located in
   ``/etc/httpd/conf/httpd.conf``
2. Add the following to the bottom:
   ``Include /etc/httpd/conf/owncloud.conf``
3. Restart apache and now when you point your browser to
   ``owncloud.foo.com`` it should properly load without disturbing *foo.com*

Gentoo
------

Basically do everything like for a standard web server (see
above).Change permissions: ``chown -R apache:apache owncloud``\        Allow .htaccess, modify ``/etc/apache2/vhosts.d/00_default_vhost.conf`` and
make sure this is in

::

    <Directory /var/www/localhost/htdocs/owncloud>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
    </Directory>

PCLinuxOS
---------

Tutorial: `ownCloud, installation and setup`_

MacOS
-----

1. Install `MAMP`_ and run it.
2. Go to ‘Preferences ? Apache’ and set ‘Document Root’ to
   ``/Users/<YOUR USER NAME>/Sites``, so your Sites directory will be
   used as Apache root.
3. Download ownCloud

   -  `latest development version`_
   -  from repository:
      ``git clone git://gitorious.org/owncloud/owncloud.git``

4. Move it to ``~/Sites`` and extract it:
   ``tar xfpj owncloud-1.2.tar.bz2``
5. Now you can set it up by going to `http://localhost:8888/owncloud`_

OpenWrt
-------

Tutorial: `ownCloud on OpenWrt`_

.. _stable version 3.0: http://aur.archlinux.org/packages.php?ID=47585
.. _development version: http://aur.archlinux.org/packages.php?ID=38767
.. _`http://127.0.0.1/owncloud/index.php`: http://127.0.0.1/owncloud/index.php
.. _ownCloud 2.0.1 openSUSE Build Service: http://software.opensuse.org/search?q=owncloud&baseproject=ALL&lang=de
.. _ownCloud, installation and setup: http://pclinuxoshelp.com/index.php/Owncloud,_installation_and_setup
.. _MAMP: http://www.mamp.info/en/index.html
.. _latest development version: http://gitorious.org/owncloud/owncloud/archive-tarball/master
.. _`http://localhost:8888/owncloud`: http://localhost:8888/owncloud
.. _ownCloud on OpenWrt: http://wiki.openwrt.org/doc/howto/owncloud