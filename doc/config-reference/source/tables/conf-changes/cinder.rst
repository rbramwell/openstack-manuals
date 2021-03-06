New, updated, and deprecated options in Newton for Block Storage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

..
  Warning: Do not edit this file. It is automatically generated and your
  changes will be overwritten. The tool to do so lives in the
  openstack-doc-tools repository.

.. list-table:: New options
   :header-rows: 1
   :class: config-ref-table

   * - Option = default value
     - (Type) Help string
   * - ``[DEFAULT] additional_retry_list =``
     - (StrOpt) FSS additional retry list, separate by ;
   * - ``[DEFAULT] backup_swift_project = None``
     - (StrOpt) Swift project/account name. Required when connecting to an auth 3.0 system
   * - ``[DEFAULT] backup_swift_project_domain = None``
     - (StrOpt) Swift project domain name. Required when connecting to an auth 3.0 system
   * - ``[DEFAULT] backup_swift_user_domain = None``
     - (StrOpt) Swift user domain name. Required when connecting to an auth 3.0 system
   * - ``[DEFAULT] backup_use_temp_snapshot = False``
     - (BoolOpt) If this is set to True, the backup_use_temp_snapshot path will be used during the backup. Otherwise, it will use backup_use_temp_volume path.
   * - ``[DEFAULT] chap = disabled``
     - (StrOpt) CHAP authentication mode, effective only for iscsi (disabled|enabled)
   * - ``[DEFAULT] clone_volume_timeout = 680``
     - (IntOpt) Create clone volume timeout.
   * - ``[DEFAULT] cluster = None``
     - (StrOpt) Name of this cluster. Used to group volume hosts that share the same backend configurations to work in HA Active-Active mode. Active-Active is not yet supported.
   * - ``[DEFAULT] connection_type = iscsi``
     - (StrOpt) Connection type to the IBM Storage Array
   * - ``[DEFAULT] coprhd_emulate_snapshot = False``
     - (BoolOpt) True | False to indicate if the storage array in CoprHD is VMAX or VPLEX
   * - ``[DEFAULT] coprhd_hostname = None``
     - (StrOpt) Hostname for the CoprHD Instance
   * - ``[DEFAULT] coprhd_password = None``
     - (StrOpt) Password for accessing the CoprHD Instance
   * - ``[DEFAULT] coprhd_port = 4443``
     - (PortOpt) Port for the CoprHD Instance
   * - ``[DEFAULT] coprhd_project = None``
     - (StrOpt) Project to utilize within the CoprHD Instance
   * - ``[DEFAULT] coprhd_scaleio_rest_gateway_host = None``
     - (StrOpt) Rest Gateway IP or FQDN for Scaleio
   * - ``[DEFAULT] coprhd_scaleio_rest_gateway_port = 4984``
     - (PortOpt) Rest Gateway Port for Scaleio
   * - ``[DEFAULT] coprhd_scaleio_rest_server_password = None``
     - (StrOpt) Rest Gateway Password
   * - ``[DEFAULT] coprhd_scaleio_rest_server_username = None``
     - (StrOpt) Username for Rest Gateway
   * - ``[DEFAULT] coprhd_tenant = None``
     - (StrOpt) Tenant to utilize within the CoprHD Instance
   * - ``[DEFAULT] coprhd_username = None``
     - (StrOpt) Username for accessing the CoprHD Instance
   * - ``[DEFAULT] coprhd_varray = None``
     - (StrOpt) Virtual Array to utilize within the CoprHD Instance
   * - ``[DEFAULT] datera_503_interval = 5``
     - (IntOpt) Interval between 503 retries
   * - ``[DEFAULT] datera_503_timeout = 120``
     - (IntOpt) Timeout for HTTP 503 retry messages
   * - ``[DEFAULT] datera_acl_allow_all = False``
     - (BoolOpt) True to set acl 'allow_all' on volumes created
   * - ``[DEFAULT] datera_debug = False``
     - (BoolOpt) True to set function arg and return logging
   * - ``[DEFAULT] datera_debug_replica_count_override = False``
     - (BoolOpt) ONLY FOR DEBUG/TESTING PURPOSES True to set replica_count to 1
   * - ``[DEFAULT] default_group_type = None``
     - (StrOpt) Default group type to use
   * - ``[DEFAULT] dell_server_os = Red Hat Linux 6.x``
     - (StrOpt) Server OS type to use when creating a new server on the Storage Center.
   * - ``[DEFAULT] drbdmanage_disk_options = {"c-min-rate": "4M"}``
     - (StrOpt) Disk options to set on new resources. See http://www.drbd.org/en/doc/users-guide-90/re-drbdconf for all the details.
   * - ``[DEFAULT] drbdmanage_net_options = {"connect-int": "4", "allow-two-primaries": "yes", "ko-count": "30", "max-buffers": "20000", "ping-timeout": "100"}``
     - (StrOpt) Net options to set on new resources. See http://www.drbd.org/en/doc/users-guide-90/re-drbdconf for all the details.
   * - ``[DEFAULT] drbdmanage_resource_options = {"auto-promote-timeout": "300"}``
     - (StrOpt) Resource options to set on new resources. See http://www.drbd.org/en/doc/users-guide-90/re-drbdconf for all the details.
   * - ``[DEFAULT] dsware_isthin = False``
     - (BoolOpt) The flag of thin storage allocation.
   * - ``[DEFAULT] dsware_manager =``
     - (StrOpt) Fusionstorage manager ip addr for cinder-volume.
   * - ``[DEFAULT] enable_unsupported_driver = False``
     - (BoolOpt) Set this to True when you want to allow an unsupported driver to start. Drivers that haven't maintained a working CI system and testing are marked as unsupported until CI is working again. This also marks a driver as deprecated and may be removed in the next release.
   * - ``[DEFAULT] fss_debug = False``
     - (BoolOpt) Enable HTTP debugging to FSS
   * - ``[DEFAULT] fss_pool =``
     - (IntOpt) FSS pool id in which FalconStor volumes are stored.
   * - ``[DEFAULT] fusionstorageagent =``
     - (StrOpt) Fusionstorage agent ip addr range.
   * - ``[DEFAULT] glance_catalog_info = image:glance:publicURL``
     - (StrOpt) Info to match when looking for glance in the service catalog. Format is: separated values of the form: <service_type>:<service_name>:<endpoint_type> - Only used if glance_api_servers are not provided.
   * - ``[DEFAULT] group_api_class = cinder.group.api.API``
     - (StrOpt) The full class name of the group API class
   * - ``[DEFAULT] hnas_chap_enabled = True``
     - (BoolOpt) Whether the chap authentication is enabled in the iSCSI target or not.
   * - ``[DEFAULT] hnas_cluster_admin_ip0 = None``
     - (StrOpt) The IP of the HNAS cluster admin. Required only for HNAS multi-cluster setups.
   * - ``[DEFAULT] hnas_mgmt_ip0 = None``
     - (IPOpt) Management IP address of HNAS. This can be any IP in the admin address on HNAS or the SMU IP.
   * - ``[DEFAULT] hnas_password = None``
     - (StrOpt) HNAS password.
   * - ``[DEFAULT] hnas_ssc_cmd = ssc``
     - (StrOpt) Command to communicate to HNAS.
   * - ``[DEFAULT] hnas_ssh_port = 22``
     - (PortOpt) Port to be used for SSH authentication.
   * - ``[DEFAULT] hnas_ssh_private_key = None``
     - (StrOpt) Path to the SSH private key used to authenticate in HNAS SMU.
   * - ``[DEFAULT] hnas_svc0_hdp = None``
     - (StrOpt) Service 0 HDP
   * - ``[DEFAULT] hnas_svc0_iscsi_ip = None``
     - (IPOpt) Service 0 iSCSI IP
   * - ``[DEFAULT] hnas_svc0_volume_type = None``
     - (StrOpt) Service 0 volume type
   * - ``[DEFAULT] hnas_svc1_hdp = None``
     - (StrOpt) Service 1 HDP
   * - ``[DEFAULT] hnas_svc1_iscsi_ip = None``
     - (IPOpt) Service 1 iSCSI IP
   * - ``[DEFAULT] hnas_svc1_volume_type = None``
     - (StrOpt) Service 1 volume type
   * - ``[DEFAULT] hnas_svc2_hdp = None``
     - (StrOpt) Service 2 HDP
   * - ``[DEFAULT] hnas_svc2_iscsi_ip = None``
     - (IPOpt) Service 2 iSCSI IP
   * - ``[DEFAULT] hnas_svc2_volume_type = None``
     - (StrOpt) Service 2 volume type
   * - ``[DEFAULT] hnas_svc3_hdp = None``
     - (StrOpt) Service 3 HDP
   * - ``[DEFAULT] hnas_svc3_iscsi_ip = None``
     - (IPOpt) Service 3 iSCSI IP
   * - ``[DEFAULT] hnas_svc3_volume_type = None``
     - (StrOpt) Service 3 volume type
   * - ``[DEFAULT] hnas_username = None``
     - (StrOpt) HNAS username.
   * - ``[DEFAULT] kaminario_nodedup_substring = K2-nodedup``
     - (StrOpt) If volume-type name contains this substring nodedup volume will be created, otherwise dedup volume wil be created.
   * - ``[DEFAULT] lvm_suppress_fd_warnings = False``
     - (BoolOpt) Suppress leaked file descriptor warnings in LVM commands.
   * - ``[DEFAULT] message_ttl = 2592000``
     - (IntOpt) message minimum life in seconds.
   * - ``[DEFAULT] metro_domain_name = None``
     - (StrOpt) The remote metro device domain name.
   * - ``[DEFAULT] metro_san_address = None``
     - (StrOpt) The remote metro device request url.
   * - ``[DEFAULT] metro_san_password = None``
     - (StrOpt) The remote metro device san password.
   * - ``[DEFAULT] metro_san_user = None``
     - (StrOpt) The remote metro device san user.
   * - ``[DEFAULT] metro_storage_pools = None``
     - (StrOpt) The remote metro device pool names.
   * - ``[DEFAULT] nas_host =``
     - (StrOpt) IP address or Hostname of NAS system.
   * - ``[DEFAULT] netapp_replication_aggregate_map = None``
     - (MultiOpt) Multi opt of dictionaries to represent the aggregate mapping between source and destination back ends when using whole back end replication. For every source aggregate associated with a cinder pool (NetApp FlexVol), you would need to specify the destination aggregate on the replication target device. A replication target device is configured with the configuration option replication_device. Specify this option as many times as you have replication devices. Each entry takes the standard dict config form: netapp_replication_aggregate_map = backend_id:<name_of_replication_device_section>,src_aggr_name1:dest_aggr_name1,src_aggr_name2:dest_aggr_name2,...
   * - ``[DEFAULT] netapp_snapmirror_quiesce_timeout = 3600``
     - (IntOpt) The maximum time in seconds to wait for existing SnapMirror transfers to complete before aborting during a failover.
   * - ``[DEFAULT] nexenta_nbd_symlinks_dir = /dev/disk/by-path``
     - (StrOpt) NexentaEdge logical path of directory to store symbolic links to NBDs
   * - ``[DEFAULT] osapi_volume_use_ssl = False``
     - (BoolOpt) Wraps the socket in a SSL context if True is set. A certificate file and key file must be specified.
   * - ``[DEFAULT] pool_id_filter =``
     - (ListOpt) Pool id permit to use.
   * - ``[DEFAULT] pool_type = default``
     - (StrOpt) Pool type, like sata-2copy.
   * - ``[DEFAULT] proxy = storage.proxy.IBMStorageProxy``
     - (StrOpt) Proxy driver that connects to the IBM Storage Array
   * - ``[DEFAULT] quota_groups = 10``
     - (IntOpt) Number of groups allowed per project
   * - ``[DEFAULT] scaleio_server_certificate_path = None``
     - (StrOpt) Server certificate path
   * - ``[DEFAULT] scaleio_verify_server_certificate = False``
     - (BoolOpt) verify server certificate
   * - ``[DEFAULT] scheduler_weight_handler = cinder.scheduler.weights.OrderedHostWeightHandler``
     - (StrOpt) Which handler to use for selecting the host/pool after weighing
   * - ``[DEFAULT] secondary_san_ip =``
     - (StrOpt) IP address of secondary DSM controller
   * - ``[DEFAULT] secondary_san_login = Admin``
     - (StrOpt) Secondary DSM user name
   * - ``[DEFAULT] secondary_san_password =``
     - (StrOpt) Secondary DSM user password name
   * - ``[DEFAULT] secondary_sc_api_port = 3033``
     - (PortOpt) Secondary Dell API port
   * - ``[DEFAULT] sio_max_over_subscription_ratio = 10.0``
     - (FloatOpt) max_over_subscription_ratio setting for the ScaleIO driver. This replaces the general max_over_subscription_ratio which has no effect in this driver.Maximum value allowed for ScaleIO is 10.0.
   * - ``[DEFAULT] storage_protocol = iscsi``
     - (StrOpt) Protocol for transferring data between host and storage back-end.
   * - ``[DEFAULT] synology_admin_port = 5000``
     - (PortOpt) Management port for Synology storage.
   * - ``[DEFAULT] synology_device_id = None``
     - (StrOpt) Device id for skip one time password check for logging in Synology storage if OTP is enabled.
   * - ``[DEFAULT] synology_one_time_pass = None``
     - (StrOpt) One time password of administrator for logging in Synology storage if OTP is enabled.
   * - ``[DEFAULT] synology_password =``
     - (StrOpt) Password of administrator for logging in Synology storage.
   * - ``[DEFAULT] synology_pool_name =``
     - (StrOpt) Volume on Synology storage to be used for creating lun.
   * - ``[DEFAULT] synology_ssl_verify = True``
     - (BoolOpt) Do certificate validation or not if $driver_use_ssl is True
   * - ``[DEFAULT] synology_username = admin``
     - (StrOpt) Administrator of Synology storage.
   * - ``[DEFAULT] violin_dedup_capable_pools =``
     - (ListOpt) Storage pools capable of dedup and other luns.(Comma separated list)
   * - ``[DEFAULT] violin_dedup_only_pools =``
     - (ListOpt) Storage pools to be used to setup dedup luns only.(Comma separated list)
   * - ``[DEFAULT] violin_iscsi_target_ips =``
     - (ListOpt) Target iSCSI addresses to use.(Comma separated list)
   * - ``[DEFAULT] violin_pool_allocation_method = random``
     - (StrOpt) Method of choosing a storage pool for a lun.
   * - ``[DEFAULT] vzstorage_default_volume_format = raw``
     - (StrOpt) Default format that will be used when creating volumes if no volume format is specified.
   * - ``[DEFAULT] zadara_default_snap_policy = False``
     - (BoolOpt) VPSA - Attach snapshot policy for volumes
   * - ``[DEFAULT] zadara_password = None``
     - (StrOpt) VPSA - Password
   * - ``[DEFAULT] zadara_use_iser = True``
     - (BoolOpt) VPSA - Use ISER instead of iSCSI
   * - ``[DEFAULT] zadara_user = None``
     - (StrOpt) VPSA - Username
   * - ``[DEFAULT] zadara_vol_encrypt = False``
     - (BoolOpt) VPSA - Default encryption policy for volumes
   * - ``[DEFAULT] zadara_vol_name_template = OS_%s``
     - (StrOpt) VPSA - Default template for VPSA volume names
   * - ``[DEFAULT] zadara_vpsa_host = None``
     - (StrOpt) VPSA - Management Host name or IP address
   * - ``[DEFAULT] zadara_vpsa_poolname = None``
     - (StrOpt) VPSA - Storage Pool assigned for volumes
   * - ``[DEFAULT] zadara_vpsa_port = None``
     - (PortOpt) VPSA - Port number
   * - ``[DEFAULT] zadara_vpsa_use_ssl = False``
     - (BoolOpt) VPSA - Use SSL connection
   * - ``[DEFAULT] zteAheadReadSize = 8``
     - (IntOpt) Cache readahead size.
   * - ``[DEFAULT] zteCachePolicy = 1``
     - (IntOpt) Cache policy. 0, Write Back; 1, Write Through.
   * - ``[DEFAULT] zteChunkSize = 4``
     - (IntOpt) Virtual block size of pool. Unit : KB. Valid value : 4, 8, 16, 32, 64, 128, 256, 512.
   * - ``[DEFAULT] zteControllerIP0 = None``
     - (IPOpt) Main controller IP.
   * - ``[DEFAULT] zteControllerIP1 = None``
     - (IPOpt) Slave controller IP.
   * - ``[DEFAULT] zteLocalIP = None``
     - (IPOpt) Local IP.
   * - ``[DEFAULT] ztePoolVoAllocatedPolicy = 0``
     - (IntOpt) Pool volume allocated policy. 0, Auto; 1, High Performance Tier First; 2, Performance Tier First; 3, Capacity Tier First.
   * - ``[DEFAULT] ztePoolVolAlarmStopAllocatedFlag = 0``
     - (IntOpt) Pool volume alarm stop allocated flag.
   * - ``[DEFAULT] ztePoolVolAlarmThreshold = 0``
     - (IntOpt) Pool volume alarm threshold. [0, 100]
   * - ``[DEFAULT] ztePoolVolInitAllocatedCapacity = 0``
     - (IntOpt) Pool volume init allocated Capacity.Unit : KB.
   * - ``[DEFAULT] ztePoolVolIsThin = False``
     - (IntOpt) Whether it is a thin volume.
   * - ``[DEFAULT] ztePoolVolMovePolicy = 0``
     - (IntOpt) Pool volume move policy.0, Auto; 1, Highest Available; 2, Lowest Available; 3, No Relocation.
   * - ``[DEFAULT] zteSSDCacheSwitch = 1``
     - (IntOpt) SSD cache switch. 0, OFF; 1, ON.
   * - ``[DEFAULT] zteStoragePool =``
     - (ListOpt) Pool name list.
   * - ``[DEFAULT] zteUserName = None``
     - (StrOpt) User name.
   * - ``[DEFAULT] zteUserPassword = None``
     - (StrOpt) User password.
   * - ``[barbican] auth_endpoint = http://localhost:5000/v3``
     - (StrOpt) Use this endpoint to connect to Keystone
   * - ``[barbican] barbican_api_version = None``
     - (StrOpt) Version of the Barbican API, for example: "v1"
   * - ``[barbican] barbican_endpoint = None``
     - (StrOpt) Use this endpoint to connect to Barbican, for example: "http://localhost:9311/"
   * - ``[barbican] number_of_retries = 60``
     - (IntOpt) Number of times to retry poll for key creation completion
   * - ``[barbican] retry_delay = 1``
     - (IntOpt) Number of seconds to wait before retrying poll for key creation completion
   * - ``[fc-zone-manager] enable_unsupported_driver = False``
     - (BoolOpt) Set this to True when you want to allow an unsupported zone manager driver to start. Drivers that haven't maintained a working CI system and testing are marked as unsupported until CI is working again. This also marks a driver as deprecated and may be removed in the next release.
   * - ``[key_manager] api_class = castellan.key_manager.barbican_key_manager.BarbicanKeyManager``
     - (StrOpt) The full class name of the key manager API class
   * - ``[key_manager] fixed_key = None``
     - (StrOpt) Fixed key returned by key manager, specified in hex

.. list-table:: New default values
   :header-rows: 1
   :class: config-ref-table

   * - Option
     - Previous default value
     - New default value
   * - ``[DEFAULT] backup_service_inithost_offload``
     - ``False``
     - ``True``
   * - ``[DEFAULT] datera_num_replicas``
     - ``1``
     - ``3``
   * - ``[DEFAULT] default_timeout``
     - ``525600``
     - ``31536000``
   * - ``[DEFAULT] glance_api_servers``
     - ``$glance_host:$glance_port``
     - ``None``
   * - ``[DEFAULT] io_port_list``
     - ``*``
     - ``None``
   * - ``[DEFAULT] iscsi_initiators``
     -
     - ``None``
   * - ``[DEFAULT] naviseccli_path``
     -
     - ``None``
   * - ``[DEFAULT] nexenta_chunksize``
     - ``16384``
     - ``32768``
   * - ``[DEFAULT] query_volume_filters``
     - ``name, status, metadata, availability_zone, bootable``
     - ``name, status, metadata, availability_zone, bootable, group_id``
   * - ``[DEFAULT] vmware_task_poll_interval``
     - ``0.5``
     - ``2.0``

.. list-table:: Deprecated options
   :header-rows: 1
   :class: config-ref-table

   * - Deprecated option
     - New Option
   * - ``[DEFAULT] enable_v1_api``
     - ``None``
   * - ``[DEFAULT] enable_v2_api``
     - ``None``
   * - ``[DEFAULT] eqlx_chap_login``
     - ``[DEFAULT] chap_username``
   * - ``[DEFAULT] eqlx_chap_password``
     - ``[DEFAULT] chap_password``
   * - ``[DEFAULT] eqlx_use_chap``
     - ``[DEFAULT] use_chap_auth``
   * - ``[DEFAULT] host``
     - ``[DEFAULT] backend_host``
   * - ``[DEFAULT] nas_ip``
     - ``[DEFAULT] nas_host``
   * - ``[DEFAULT] osapi_max_request_body_size``
     - ``[oslo_middleware] max_request_body_size``
   * - ``[DEFAULT] use_syslog``
     - ``None``
   * - ``[hyperv] force_volumeutils_v1``
     - ``None``

