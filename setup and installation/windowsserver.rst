Windows Server
==============
Please note: You must move the data directory outside of your public root. (See advanced install settings)

How to install ownCloud on Windows 7
------------------------------------

To Start:
~~~~~~~~~

First, this assumes that you have a vanilla, non-IIS enabled Windows
machine – Windows 7 or Server 2008. After enabling IIS, the steps are
essentially identical for Windows 7 and Windows Server 2008. You must install this on 
machine you have physical access to, though that is not strictly necessary, a remote
desktop connection will suffice. You should leverage 
MySQL as the back end database for ownCloud.  If you do not want to use
MySQL, it is possible to use postgres or SQLite instead. This tutorial will not tech you to 
install a certificate to enable SSL, that will
be a later, more advanced addition to this tutorial later. Please note,
if you make this web server available to the outside world, you must
maintain it. Monitor the logs, manage the access, apply patches –
because you run a risk and a bit of a hassle if you do not. **Lets get
started.**

Overview:
~~~~~~~~~

There are 4 primary steps to the installation, and then a 5th step
required for configuring everything to allow files larger than the
default 2MB. 

1. Install IIS with CGI support – enable IIS on your Windows machine.

2. Install PHP – Grab, download and install PHP. 

3. Install MySQL – Setup the MySQL server manager and enable ownCloud to create an instance. 

4. Install ownCloud – The whole reason we are here!

5. Configure upload sizes and timeouts to enable large file uploads – So that you can upload larger files.

Part 1: Activate IIS with CGI Support
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Windows 7
"""""""""
1. Go to Start > Control Panel > Programs. 

2. Under Programs and Features, there is link titled ``Turn Windows Features on and Off``. Click on it. 

3. There is a box labeled Internet Information Services, expand it. 

4. Expand World Wide Web Services and all the folders underneath. 

5. Select the folders as illustrated in the picture below to get your IIS server up and running. 

                                                                                            

                    .. image:: /images/winserver.jpeg

You don’t need an FTP server running, so you should tune
that feature off for your server. You definitely need the IIS Management
Console, as that is the easiest way to start, stop, restart you server,
as well as where you change certificate options and manage items like
file upload size. You must check the CGI box under Application
Development Features, because CGI is how you enable PHP on IIS. You have to turn off WebDAV 

publishing or the Windows WebDAV
conflicts with the ownCloud WebDAV interface. This might already be
turned off for you, just make sure it stays that way. The common HTTP
features are, as you might expect from the name, the features you would
expect from a web server. With the selections on this page, IIS will now
serve up a web page for you. Restart IIS by going to the IIS manager
(Start > IIS Manager). Select your website, and on the far right side is
a section titled Manage Server. Make sure that the service is started,
or click “Start” to start the services selected. Once this is complete,
you should be able to go to a web browser and type in “localhost”. This
should open the standard IIS 7 splash page, which is just a static image
that says your web server is running. Assuming you were able to get the
splash page, it is safe to say your web server is now up and running.
The next part of this how to starts getting PHP installed on the
server.


Windows Server 2008
"""""""""""""""""""""""

1. Go to Start > Control Panel > Programs. 

2. Under Programs and Features, there is link titled ``Turn Windows Features on and Off``. Click on it.

3. This will bring up the Server Manager.

4. In the server manager, Click on Roles, and then click Add Roles. 

5. Use the "Add Roles Wizard" to add the web server role.
 
.. image:: /images/winserver1.jpg


6. Make sure that, at a minimum, the same boxes are checked in this wizard that are checked in the Windows 7 Section. For example, make sure that the CGI box is checked under Application Development Features, and that WebDAV Publishing is turned off. With Remote Desktop Sharing turned on, the detailed role service list looks like the figure “Role Services”. 

7. Restart IIS by going to the IIS manager (Start > IIS Manager). 

8. Select your website, and on the far right side is a section titled Manage Server. Make sure that the service is started, or click “Start” to start the services selected. 

9. Once this is complete, you should be able to go to a web browser and type in “localhost”. This should open the standard IIS 7 splash page, which is just a static image that says your web server is running.Assuming you were able to get the splash page, it is safe to say your web server is now up and running. The next part of this “how to” installs PHP on the server.

Part 2: Installing PHP
~~~~~~~~~~~~~~~~~~~~~~

This part is also straightforward, but it is necessary to remind you that this is for IIS 
only. 

1. Go to the following link and grab the PHP installer for version VC9 Non Thread Safe 32 or 64 bit based on your system. http://windows.php.net/download/ 

*Note: if you are using Apache, make sure you grab VC6 instead, lower on the page.*
You may have to log in at this point.


2. Once through that login, select the location that is closest to you geographically.


3. Run that install wizard once it is downloaded. Read the license agreement, agree, select an install directory.

4. Then select IIS FastCGI as the install server. 

5. Take the default selections for the items to install, and click next. Then click  install. 

6. And, after a few minutes, PHP will be installed. On to MySQL.

Part 3: Installing MySQL
~~~~~~~~~~~~~~~~~~~~~~~~

This part installs mySQL on your Windows machine.


1. Point your browser over to http://dev.mysql.com/downloads/ and download the latest community edition for your OS – the 32 or 64 bit version. Please download the ``MSI Installer`` as it will make life easier.

2. Once downloaded, install MySQL (5.5 at the time of writing). Select the Typical installation. 

3. When that finishes, check the box to launch the MySQL Instance Configuration Wizard and click Finish. 

4. Select a standard configuration, as this will be the only version of MySQL on this machine. 

5. Select to install as a windows service, and Check the Launch the MySQL Server Automatically button. 

6. Select the modify security settings box on the next page, and enter a password you will remember. You will need this password when you configure ownCloud. 

7. Uncheck ``enable`` root access from remote machines” for security reasons. 

8. Click execute, and wait while the instance is created and launched. 

9. Click Finish when this is all complete.


You can make some pretty good educated guesses on
the type of install needed for ownCloud. Take particular note of your
MySQL password, as the username root and the password you select will be
necessary alter on in the ownCloud installation. As an aside, this link
is an excellent resource for questions on how to configure your MySQL
instance, and also to configure PHP to work with MySQL. This, however,
is not strictly necessary as much of this is handled when you download
ownCloud. 

http://learn.iis.net/page.aspx/353/install-and-configure-mysql-for-php-applications-on-iis-7-and-above/

Part 4: Installing ownCloud
~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Download the latest version of ownCloud from http://owncloud.org/download . 

2. It will arrive as a tar.bz2 file, and I recommend something like jZip for a free utility to unzip it. 

3. Once you have the owncloud directory unzipped and saved locally, copy it into your wwwroot directory (probably ``c:\\inetpub\\wwwroot``). 

*Why not install it directly into the directory ``wwwroot`` from jzip? It has to do with permissions, and only the admin can unzip into the ``wwwroot`` directory, if that. If you save it in a different folder, and then move the files into ``wwwroot`` in Windows explorer, it works.This will install ownCloud locally in your root web directory. You can use a subdirectory called owncloud, or whatever you want – the www root, or something 
else.*

4. It is now time to give write access to the ownCloud directory to the owncloud server. 

 Navigate your windows explorer over to ``inetpub/wwwroot/owncloud`` (or your installation directory if you selected something different). 

5. Right click and select properties. Click on the security tab, and click the button “to change permissions, click edit”. 

6. Select the “users” user from the list, and check the box “write”. 

7. Apply these settings and close out.

8. Now open your browser and go to ``http://localhost/owncloud`` (or localhost if it is installed in the root www directory). This should bring up the ownCloud configuration page. 

9. At this page, you enter your desired ownCloud username and password for the administrator, and expand the little arrow. 

10. Select MySQL as the database, and enter your MySQL database username, password and desired instance name – use the username and password you setup for MySQL earlier in step 3, and pick any name for the database instance.

*Note: the owncloud admin password and the MySQL password CANNOT be the same in any way.*

11. Click next, and ownCloud should have you logged in as the admin user, and you can get started exploring ownCloud, creating other users and more! 

Part 5: Configuring ownCloud, PHP and IIS for Large File Uploads
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Before going too nuts on ownCloud, it is important to do a couple config changes to make 
this a useful service for you. You will probably want to increase the ``max upload size``, 
for example. The default upload is set to ``2MB``, which is too small for even most MP3 
files. 

To do that, simply go into your PHP.ini file, which can be found in your ``c:/Program Files (x86) / PHP folder``. In here, you will find a ``PHP.ini file``. Open this in
a text editor, and look for a few key attributes to change: 

+ ``upload_max_filesize`` – change this to something good, like 1G, and you will get to 

upload much larger files. 

+ ``post_max_size`` – also change this size, and make it larger than the max upload size you chose, like 1G.

There are other changes you can make, such as the timeout duration for
uploads, but for now you should be all set in the PHP.ini file.

Now you
have to go back to IIS manager and make one last change to enable file
uploads on the webserver larger than 30MB.

1. Go to the start menu, and type in iis manager. 

2. Open IIS Manager Select the website you want enable to accept large file uploads. 

3. In the main window in the middle double click on the icon ``Request filtering``. 

4. Once the window is opened you will see a bunch of tabs across the top of the far right, 

 select ``Edit Feature Settings`` and modify the ``Maximum allowed content length (bytes)`` 

5. In here, you can change this to up to 4.1 GB. 

*Note, this entry is in BYTES, not KB.*



And that is it. You should now have ownCloud configured and ready
for you to play with.