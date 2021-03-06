.. _keystone-install:

Install and configure
~~~~~~~~~~~~~~~~~~~~~

This section describes how to install and configure the OpenStack
Identity service, code-named keystone, on the controller node. For
scalability purposes, this configuration deploys Fernet tokens and
the Apache HTTP server to handle requests.

Prerequisites
-------------

Before you configure the OpenStack Identity service, you must create a
database and an administration token.

#. To create the database, complete the following actions:

   * Use the database access client to connect to the database server as the
     ``root`` user:

     .. code-block:: console

        $ mysql -u root -p

     .. end

   * Create the ``keystone`` database:

     .. code-block:: console

        mysql> CREATE DATABASE keystone;

     .. end

   * Grant proper access to the ``keystone`` database:

     .. code-block:: console

        mysql> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' \
          IDENTIFIED BY 'KEYSTONE_DBPASS';
        mysql> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' \
          IDENTIFIED BY 'KEYSTONE_DBPASS';

     .. end

     Replace ``KEYSTONE_DBPASS`` with a suitable password.

   * Exit the database access client.

Install and configure components
--------------------------------

.. include:: shared/note_configuration_vary_by_distribution.rst

.. only:: obs or rdo

   .. note::

      This guide uses the Apache HTTP server with ``mod_wsgi`` to serve
      Identity service requests on ports 5000 and 35357. By default, the
      keystone service still listens on these ports. Therefore, this guide
      manually disables the keystone service.

.. endonly

.. only:: ubuntu or debian

   .. note::

      This guide uses the Apache HTTP server with ``mod_wsgi`` to serve
      Identity service requests on ports 5000 and 35357. By default, the
      keystone service still listens on these ports. The package handles
      all of the Apache configuration for you (including the activation of
      the ``mod_wsgi`` apache2 module and keystone configuration in Apache).

   #. Run the following command to install the packages:

      .. code-block:: console

         # apt-get install keystone

      .. end

.. endonly


.. only:: rdo

    #. Run the following command to install the packages:

         .. code-block:: console

            # yum install openstack-keystone httpd mod_wsgi

         .. end

.. endonly

.. only:: obs

    #. Run the following command to install the packages:

         .. code-block:: console

            # zypper install openstack-keystone apache2-mod_wsgi

         .. end

.. endonly

2. Edit the ``/etc/keystone/keystone.conf`` file and complete the following
   actions:

   * In the ``[database]`` section, configure database access:

     .. path /etc/keystone/keystone.conf
     .. code-block:: ini

        [database]
        ...
        connection = mysql+pymysql://keystone:KEYSTONE_DBPASS@controller/keystone

     .. end

     Replace ``KEYSTONE_DBPASS`` with the password you chose for the database.

   * In the ``[token]`` section, configure the Fernet token provider:

     .. path /etc/keystone/keystone.conf
     .. code-block:: ini

        [token]
        ...
        provider = fernet

     .. end

3. Populate the Identity service database:

   .. code-block:: console

      # su -s /bin/sh -c "keystone-manage db_sync" keystone

   .. end

   .. note::

     Ignore any deprecation messages in this output.

4. Initialize Fernet key repositories:

   .. code-block:: console

      # keystone-manage fernet_setup --keystone-user keystone --keystone-group keystone
      # keystone-manage credential_setup --keystone-user keystone --keystone-group keystone

   .. end

5. Bootstrap the Identity service:

   .. code-block:: console

      # keystone-manage bootstrap --bootstrap-password ADMIN_PASSWORD \
        --bootstrap-admin-url http://controller:35357/v3/ \
        --bootstrap-internal-url http://controller:35357/v3/ \
        --bootstrap-public-url http://controller:5000/v3/ \
        --bootstrap-region-id RegionOne

   .. end

   Replace ``ADMIN_PASSWORD`` with a suitable password for an administrative user.

.. only:: rdo

   Configure the Apache HTTP server
   --------------------------------

   #. Edit the ``/etc/httpd/conf/httpd.conf`` file and configure the
      ``ServerName`` option to reference the controller node:

      #. Edit the ``/etc/httpd/conf/httpd.conf`` file and configure the
         ``ServerName`` option to reference the controller node:

         .. path /etc/httpd/conf/httpd
         .. code-block:: apache

            ServerName controller

         .. end

      #. Create the ``/etc/httpd/conf.d/wsgi-keystone.conf`` file with
         the following content:

         .. path /etc/httpd/conf.d/wsgi-keystone.conf
         .. code-block:: apache

            Listen 5000
            Listen 35357

            <VirtualHost *:5000>
                WSGIDaemonProcess keystone-public processes=5 threads=1 user=keystone group=keystone display-name=%{GROUP}
                WSGIProcessGroup keystone-public
                WSGIScriptAlias / /usr/bin/keystone-wsgi-public
                WSGIApplicationGroup %{GLOBAL}
                WSGIPassAuthorization On
                ErrorLogFormat "%{cu}t %M"
                ErrorLog /var/log/httpd/keystone-error.log
                CustomLog /var/log/httpd/keystone-access.log combined

                <Directory /usr/bin>
                    Require all granted
                </Directory>
            </VirtualHost>

            <VirtualHost *:35357>
                WSGIDaemonProcess keystone-admin processes=5 threads=1 user=keystone group=keystone display-name=%{GROUP}
                WSGIProcessGroup keystone-admin
                WSGIScriptAlias / /usr/bin/keystone-wsgi-admin
                WSGIApplicationGroup %{GLOBAL}
                WSGIPassAuthorization On
                ErrorLogFormat "%{cu}t %M"
                ErrorLog /var/log/httpd/keystone-error.log
                CustomLog /var/log/httpd/keystone-access.log combined

                <Directory /usr/bin>
                    Require all granted
                </Directory>
            </VirtualHost>

        .. end

.. endonly

   .. only:: ubuntu

      #. Edit the ``/etc/apache2/apache2.conf`` file and configure the
         ``ServerName`` option to reference the controller node:

         .. path /etc/apache2/apache2.conf
         .. code-block:: apache

            ServerName controller

         .. end

      #. Create the ``/etc/apache2/sites-available/wsgi-keystone.conf`` file
         with the following content:

         .. path /etc/apache2/sites-available/wsgi-keystone.conf
         .. code-block:: apache

            Listen 5000
            Listen 35357

            <VirtualHost *:5000>
                WSGIDaemonProcess keystone-public processes=5 threads=1 user=keystone group=keystone display-name=%{GROUP}
                WSGIProcessGroup keystone-public
                WSGIScriptAlias / /usr/bin/keystone-wsgi-public
                WSGIApplicationGroup %{GLOBAL}
                WSGIPassAuthorization On
                ErrorLogFormat "%{cu}t %M"
                ErrorLog /var/log/apache2/keystone.log
                CustomLog /var/log/apache2/keystone_access.log combined

                <Directory /usr/bin>
                    Require all granted
                </Directory>
            </VirtualHost>

            <VirtualHost *:35357>
                WSGIDaemonProcess keystone-admin processes=5 threads=1 user=keystone group=keystone display-name=%{GROUP}
                WSGIProcessGroup keystone-admin
                WSGIScriptAlias / /usr/bin/keystone-wsgi-admin
                WSGIApplicationGroup %{GLOBAL}
                WSGIPassAuthorization On
                ErrorLogFormat "%{cu}t %M"
                ErrorLog /var/log/apache2/keystone.log
                CustomLog /var/log/apache2/keystone_access.log combined

                <Directory /usr/bin>
                    Require all granted
                </Directory>
            </VirtualHost>

         .. end

      #. Enable the Identity service virtual hosts:

         .. code-block:: console

            # ln -s /etc/apache2/sites-available/wsgi-keystone.conf /etc/apache2/sites-enabled

         .. end

   .. endonly

   .. only:: obs

      #. Edit the ``/etc/sysconfig/apache2`` file and configure the
         ``APACHE_SERVERNAME`` option to reference the controller node:

         .. path /etc/sysconfig/apache2
         .. code-block:: apache

            APACHE_SERVERNAME="controller"

         .. end

      #. Create the ``/etc/apache2/conf.d/wsgi-keystone.conf`` file
         with the following content:

         .. path /etc/apache2/conf.d/wsgi-keystone.conf
         .. code-block:: apache

            Listen 5000
            Listen 35357

            <VirtualHost *:5000>
                WSGIDaemonProcess keystone-public processes=5 threads=1 user=keystone group=keystone display-name=%{GROUP}
                WSGIProcessGroup keystone-public
                WSGIScriptAlias / /usr/bin/keystone-wsgi-public
                WSGIApplicationGroup %{GLOBAL}
                WSGIPassAuthorization On
                ErrorLogFormat "%{cu}t %M"
                ErrorLog /var/log/apache2/keystone.log
                CustomLog /var/log/apache2/keystone_access.log combined

                <Directory /usr/bin>
                    Require all granted
                </Directory>
            </VirtualHost>

            <VirtualHost *:35357>
                WSGIDaemonProcess keystone-admin processes=5 threads=1 user=keystone group=keystone display-name=%{GROUP}
                WSGIProcessGroup keystone-admin
                WSGIScriptAlias / /usr/bin/keystone-wsgi-admin
                WSGIApplicationGroup %{GLOBAL}
                WSGIPassAuthorization On
                ErrorLogFormat "%{cu}t %M"
                ErrorLog /var/log/apache2/keystone.log
                CustomLog /var/log/apache2/keystone_access.log combined

                <Directory /usr/bin>
                    Require all granted
                </Directory>
            </VirtualHost>

         .. end

      6. Recursively change the ownership of the ``/etc/keystone`` directory:

         .. code-block:: console

            # chown -R keystone:keystone /etc/keystone

         .. end

   .. endonly

.. only:: ubuntu or rdo or obs

   Finalize the installation
   -------------------------

.. endonly

   .. only:: ubuntu

      .. code-block:: console

         # service apache2 restart

      .. end

   #. By default, the Ubuntu packages create an SQLite database.

      #. By default, the Ubuntu packages create an SQLite database.

      .. code-block:: console

         # rm -f /var/lib/keystone/keystone.db

      .. end

   .. endonly

   .. only:: rdo

     .. code-block:: console

        # systemctl enable httpd.service
        # systemctl start httpd.service

     .. end

   .. endonly

   .. only:: obs

      #. Start the Apache HTTP service and configure it to start when the system boots:

         .. code-block:: console

            # systemctl enable apache2.service
            # systemctl start apache2.service

         .. end

   .. endonly

6. Configure the administrative account

   .. code-block:: console

      $ export OS_USERNAME=admin
      $ export OS_PASSWORD=ADMIN_PASSWORD
      $ export OS_PROJECT_NAME=admin
      $ export OS_USER_DOMAIN_NAME=Default
      $ export OS_PROJECT_DOMAIN_NAME=Default
      $ export OS_AUTH_URL=http://controller:35357/v3
      $ export OS_IDENTITY_API_VERSION=3

   .. end

   .. only:: obs or rdo or ubuntu

      Replace ``ADMIN_PASSWORD`` with the password used in the
      ``keystone-manage bootstrap`` command from the section called
      :ref:`keystone-install`.

   .. endonly
