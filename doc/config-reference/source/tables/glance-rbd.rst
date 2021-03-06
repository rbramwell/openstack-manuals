..
    Warning: Do not edit this file. It is automatically generated from the
    software project's code and your changes will be overwritten.

    The tool to generate this file lives in openstack-doc-tools repository.

    Please make any changes needed in the code, then run the
    autogenerate-config-doc tool from the openstack-doc-tools repository, or
    ask for help on the documentation mailing list, IRC channel or meeting.

.. _glance-rbd:

.. list-table:: Description of RADOS Block Devices (RBD) configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - **[glance_store]**
     -
   * - ``rados_connect_timeout`` = ``0``
     - (Integer) Timeout value for connecting to Ceph cluster.$sentinal$This configuration option takes in the timeout value in seconds used when connecting to the Ceph cluster i.e. it sets the time to wait for glance-api before closing the connection. This prevents glance-api hangups during the connection to RBD. If the value for this option is set to less than or equal to 0, no timeout is set and the default librados value is used.$sentinal$Possible Values: * Any integer value$sentinal$Related options: * None
   * - ``rbd_store_ceph_conf`` = ``/etc/ceph/ceph.conf``
     - (String) Ceph configuration file path.$sentinal$This configuration option takes in the path to the Ceph configuration file to be used. If the value for this option is not set by the user or is set to None, librados will locate the default configuration file which is located at /etc/ceph/ceph.conf. If using Cephx authentication, this file should include a reference to the right keyring in a client.<USER> section$sentinal$Possible Values: * A valid path to a configuration file$sentinal$Related options: * rbd_store_user
   * - ``rbd_store_chunk_size`` = ``8``
     - (Integer) Size, in megabytes, to chunk RADOS images into.$sentinal$Provide an integer value representing the size in megabytes to chunk Glance images into. The default chunk size is 8 megabytes. For optimal performance, the value should be a power of two.$sentinal$When Ceph's RBD object storage system is used as the storage backend for storing Glance images, the images are chunked into objects of the size set using this option. These chunked objects are then stored across the distributed block data store to use for Glance.$sentinal$Possible Values: * Any positive integer value$sentinal$Related options: * None
   * - ``rbd_store_pool`` = ``images``
     - (String) RADOS pool in which images are stored.$sentinal$When RBD is used as the storage backend for storing Glance images, the images are stored by means of logical grouping of the objects (chunks of images) into a ``pool``. Each pool is defined with the number of placement groups it can contain. The default pool that is used is 'images'.$sentinal$More information on the RBD storage backend can be found here: http://ceph.com/planet/how-data-is-stored-in-ceph-cluster/$sentinal$Possible Values: * A valid pool name$sentinal$Related options: * None
   * - ``rbd_store_user`` = ``None``
     - (String) RADOS user to authenticate as.$sentinal$This configuration option takes in the RADOS user to authenticate as. This is only needed when RADOS authentication is enabled and is applicable only if the user is using Cephx authentication. If the value for this option is not set by the user or is set to None, a default value will be chosen, which will be based on the client. section in rbd_store_ceph_conf.$sentinal$Possible Values: * A valid RADOS user$sentinal$Related options: * rbd_store_ceph_conf
