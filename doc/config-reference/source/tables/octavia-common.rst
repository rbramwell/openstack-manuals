..
    Warning: Do not edit this file. It is automatically generated from the
    software project's code and your changes will be overwritten.

    The tool to generate this file lives in openstack-doc-tools repository.

    Please make any changes needed in the code, then run the
    autogenerate-config-doc tool from the openstack-doc-tools repository, or
    ask for help on the documentation mailing list, IRC channel or meeting.

.. _octavia-common:

.. list-table:: Description of common configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - **[DEFAULT]**
     -
   * - ``allow_bulk`` = ``True``
     - (Boolean) Allow the usage of the bulk API
   * - ``allow_pagination`` = ``False``
     - (Boolean) Allow the usage of the pagination
   * - ``allow_sorting`` = ``False``
     - (Boolean) Allow the usage of the sorting
   * - ``api_extensions_path`` =
     - (String) The path for API extensions
   * - ``api_handler`` = ``queue_producer``
     - (String) The handler that the API communicates with
   * - ``api_paste_config`` = ``api-paste.ini``
     - (String) The API paste config file to use
   * - ``auth_strategy`` = ``keystone``
     - (String) The type of authentication to use
   * - ``bind_host`` = ``0.0.0.0``
     - (Unknown) The host IP to bind to
   * - ``bind_port`` = ``9876``
     - (Port number) The port to bind to
   * - ``control_exchange`` = ``octavia``
     - (String) The default exchange under which topics are scoped. May be overridden by an exchange name specified in the transport_url option.
   * - ``executor_thread_pool_size`` = ``64``
     - (Integer) Size of executor thread pool.
   * - ``host`` = ``localhost``
     - (String) The hostname Octavia is running on
   * - ``octavia_plugins`` = ``hot_plug_plugin``
     - (String) Name of the controller plugin to use
   * - ``pagination_max_limit`` = ``-1``
     - (String) The maximum number of items returned in a single response. The string 'infinite' or a negative integer value means 'no limit'
   * - **[amphora_agent]**
     -
   * - ``agent_server_ca`` = ``/etc/octavia/certs/client_ca.pem``
     - (String) The ca which signed the client certificates
   * - ``agent_server_cert`` = ``/etc/octavia/certs/server.pem``
     - (String) The server certificate for the agent.py server to use
   * - ``agent_server_network_dir`` = ``/etc/netns/amphora-haproxy/network/interfaces.d/``
     - (String) The directory where new network interfaces are located
   * - ``agent_server_network_file`` = ``None``
     - (String) The file where the network interfaces are located. Specifying this will override any value set for agent_server_network_dir.
   * - ``amphora_id`` = ``None``
     - (String) The amphora ID.
   * - **[anchor]**
     -
   * - ``password`` = ``None``
     - (String) Anchor password
   * - ``url`` = ``http://localhost:9999/v1/sign/default``
     - (String) Anchor URL
   * - ``username`` = ``None``
     - (String) Anchor username
   * - **[certificates]**
     -
   * - ``barbican_auth`` = ``barbican_acl_auth``
     - (String) Name of the Barbican authentication method to use
   * - ``ca_certificate`` = ``/etc/ssl/certs/ssl-cert-snakeoil.pem``
     - (String) Absolute path to the CA Certificate for signing. Defaults to env[OS_OCTAVIA_TLS_CA_CERT].
   * - ``ca_private_key`` = ``/etc/ssl/private/ssl-cert-snakeoil.key``
     - (String) Absolute path to the Private Key for signing. Defaults to env[OS_OCTAVIA_TLS_CA_KEY].
   * - ``ca_private_key_passphrase`` = ``None``
     - (String) Passphrase for the Private Key. Defaults to env[OS_OCTAVIA_CA_KEY_PASS] or None.
   * - ``cert_generator`` = ``local_cert_generator``
     - (String) Name of the cert generator to use
   * - ``cert_manager`` = ``barbican_cert_manager``
     - (String) Name of the cert manager to use
   * - ``endpoint_type`` = ``publicURL``
     - (String) The endpoint_type to be used for barbican service.
   * - ``region_name`` = ``None``
     - (String) Region in Identity service catalog to use for communication with the barbican service.
   * - ``signing_digest`` = ``sha256``
     - (String) Certificate signing digest. Defaults to env[OS_OCTAVIA_CA_SIGNING_DIGEST] or "sha256".
   * - ``storage_path`` = ``/var/lib/octavia/certificates/``
     - (String) Absolute path to the certificate storage directory. Defaults to env[OS_OCTAVIA_TLS_STORAGE].
   * - **[controller_worker]**
     -
   * - ``amp_active_retries`` = ``10``
     - (Integer) Retry attempts to wait for Amphora to become active
   * - ``amp_active_wait_sec`` = ``10``
     - (Integer) Seconds to wait between checks on whether an Amphora has become active
   * - ``amp_boot_network_list`` =
     - (List) List of networks to attach to the Amphorae. All networks defined in the list will be attached to each amphora.
   * - ``amp_flavor_id`` =
     - (String) Nova instance flavor id for the Amphora
   * - ``amp_image_id`` =
     - (String) DEPRECATED: Glance image id for the Amphora image to boot Superseded by amp_image_tag option.
   * - ``amp_image_tag`` =
     - (String) Glance image tag for the Amphora image to boot. Use this option to be able to update the image without reconfiguring Octavia. Ignored if amp_image_id is defined.
   * - ``amp_network`` =
     - (String) DEPRECATED: Network to attach to the Amphorae. Replaced by amp_boot_network_list.
   * - ``amp_secgroup_list`` =
     - (List) List of security groups to attach to the Amphora.
   * - ``amp_ssh_access_allowed`` = ``True``
     - (Boolean) Determines whether or not to allow access to the Amphorae
   * - ``amp_ssh_key_name`` =
     - (String) SSH key name used to boot the Amphora
   * - ``amphora_driver`` = ``amphora_noop_driver``
     - (String) Name of the amphora driver to use
   * - ``cert_generator`` = ``local_cert_generator``
     - (String) Name of the cert generator to use
   * - ``client_ca`` = ``/etc/octavia/certs/ca_01.pem``
     - (String) Client CA for the amphora agent to use
   * - ``compute_driver`` = ``compute_noop_driver``
     - (String) Name of the compute driver to use
   * - ``loadbalancer_topology`` = ``SINGLE``
     - (String) Load balancer topology configuration. SINGLE - One amphora per load balancer. ACTIVE_STANDBY - Two amphora per load balancer.
   * - ``network_driver`` = ``network_noop_driver``
     - (String) Name of the network driver to use
   * - ``user_data_config_drive`` = ``False``
     - (Boolean) If True, build cloud-init user-data that is passed to the config drive on Amphora boot instead of personality files. If False, utilize personality files.
   * - **[glance]**
     -
   * - ``ca_certificates_file`` = ``None``
     - (String) CA certificates file path
   * - ``endpoint`` = ``None``
     - (String) A new endpoint to override the endpoint in the keystone catalog.
   * - ``endpoint_type`` = ``publicURL``
     - (String) Endpoint interface in identity service to use
   * - ``insecure`` = ``False``
     - (Boolean) Disable certificate validation on SSL connections
   * - ``region_name`` = ``None``
     - (String) Region in Identity service catalog to use for communication with the OpenStack services.
   * - ``service_name`` = ``None``
     - (String) The name of the glance service in the keystone catalog
   * - **[haproxy_amphora]**
     -
   * - ``base_cert_dir`` = ``/var/lib/octavia/certs``
     - (String) Base directory for cert storage.
   * - ``base_path`` = ``/var/lib/octavia``
     - (String) Base directory for amphora files.
   * - ``bind_host`` = ``0.0.0.0``
     - (Unknown) The host IP to bind to
   * - ``bind_port`` = ``9443``
     - (Port number) The port to bind to
   * - ``client_cert`` = ``/etc/octavia/certs/client.pem``
     - (String) The client certificate to talk to the agent
   * - ``connection_max_retries`` = ``300``
     - (Integer) Retry threshold for connecting to amphorae.
   * - ``connection_retry_interval`` = ``5``
     - (Integer) Retry timeout between connection attempts in seconds.
   * - ``haproxy_cmd`` = ``/usr/sbin/haproxy``
     - (String) The full path to haproxy
   * - ``haproxy_stick_size`` = ``10k``
     - (String) Size of the HAProxy stick table. Accepts k, m, g suffixes. Example: 10k
   * - ``haproxy_template`` = ``None``
     - (String) Custom haproxy template.
   * - ``respawn_count`` = ``2``
     - (Integer) The respawn count for haproxy's upstart script
   * - ``respawn_interval`` = ``2``
     - (Integer) The respawn interval for haproxy's upstart script
   * - ``rest_request_conn_timeout`` = ``10``
     - (Floating point) The time in seconds to wait for a REST API to connect.
   * - ``rest_request_read_timeout`` = ``60``
     - (Floating point) The time in seconds to wait for a REST API response.
   * - ``server_ca`` = ``/etc/octavia/certs/server_ca.pem``
     - (String) The ca which signed the server certificates
   * - ``use_upstart`` = ``True``
     - (Boolean) If False, use sysvinit.
   * - **[health_manager]**
     -
   * - ``bind_ip`` = ``0.0.0.0``
     - (Unknown) IP address the controller will listen on for heart beats
   * - ``bind_port`` = ``5555``
     - (Port number) Port number the controller will listen onfor heart beats
   * - ``controller_ip_port_list`` =
     - (List) List of controller ip and port pairs for the heartbeat receivers. Example 127.0.0.1:5555, 192.168.0.1:5555
   * - ``event_streamer_driver`` = ``noop_event_streamer``
     - (String) Specifies which driver to use for the event_streamer for syncing the octavia and neutron_lbaas dbs. If you don't need to sync the database or are running octavia in stand alone mode use the noop_event_streamer
   * - ``failover_threads`` = ``10``
     - (Integer) Number of threads performing amphora failovers.
   * - ``health_check_interval`` = ``3``
     - (Integer) Sleep time between health checks in seconds.
   * - ``heartbeat_interval`` = ``10``
     - (Integer) Sleep time between sending heartbeats.
   * - ``heartbeat_key`` = ``None``
     - (String) key used to validate amphora sendingthe message
   * - ``heartbeat_timeout`` = ``60``
     - (Integer) Interval, in seconds, to wait before failing over an amphora.
   * - ``sock_rlimit`` = ``0``
     - (Integer) sets the value of the heartbeat recv buffer
   * - ``status_update_threads`` = ``50``
     - (Integer) Number of threads performing amphora status update.
   * - **[house_keeping]**
     -
   * - ``amphora_expiry_age`` = ``604800``
     - (Integer) Amphora expiry age in seconds
   * - ``cert_expiry_buffer`` = ``1209600``
     - (Integer) Seconds until certificate expiration
   * - ``cert_interval`` = ``3600``
     - (Integer) Certificate check interval in seconds
   * - ``cert_rotate_threads`` = ``10``
     - (Integer) Number of threads performing amphora certificate rotation
   * - ``cleanup_interval`` = ``30``
     - (Integer) DB cleanup interval in seconds
   * - ``load_balancer_expiry_age`` = ``604800``
     - (Integer) Load balancer expiry age in seconds
   * - ``spare_amphora_pool_size`` = ``0``
     - (Integer) Number of spare amphorae
   * - ``spare_check_interval`` = ``30``
     - (Integer) Spare check interval in seconds
   * - **[keepalived_vrrp]**
     -
   * - ``vrrp_advert_int`` = ``1``
     - (Integer) Amphora role and priority advertisement interval in seconds.
   * - ``vrrp_check_interval`` = ``5``
     - (Integer) VRRP health check script run interval in seconds.
   * - ``vrrp_fail_count`` = ``2``
     - (Integer) Number of successive failures before transition to a fail state.
   * - ``vrrp_garp_refresh_count`` = ``2``
     - (Integer) Number of gratuitous ARP announcements to make on each refresh interval.
   * - ``vrrp_garp_refresh_interval`` = ``5``
     - (Integer) Time in seconds between gratuitous ARP announcements from the MASTER.
   * - ``vrrp_success_count`` = ``2``
     - (Integer) Number of consecutive successes before transition to a success state.
   * - **[networking]**
     -
   * - ``lb_network_name`` = ``None``
     - (String) Name of amphora internal network
   * - ``max_retries`` = ``15``
     - (Integer) The maximum attempts to retry an action with the networking service.
   * - ``port_detach_timeout`` = ``300``
     - (Integer) Seconds to wait for a port to detach from an amphora.
   * - ``retry_interval`` = ``1``
     - (Integer) Seconds to wait before retrying an action with the networking service.
   * - **[neutron]**
     -
   * - ``ca_certificates_file`` = ``None``
     - (String) CA certificates file path
   * - ``endpoint`` = ``None``
     - (String) A new endpoint to override the endpoint in the keystone catalog.
   * - ``endpoint_type`` = ``publicURL``
     - (String) Endpoint interface in identity service to use
   * - ``insecure`` = ``False``
     - (Boolean) Disable certificate validation on SSL connections
   * - ``region_name`` = ``None``
     - (String) Region in Identity service catalog to use for communication with the OpenStack services.
   * - ``service_name`` = ``None``
     - (String) The name of the neutron service in the keystone catalog
   * - **[nova]**
     -
   * - ``ca_certificates_file`` = ``None``
     - (String) CA certificates file path
   * - ``enable_anti_affinity`` = ``False``
     - (Boolean) Flag to indicate if nova anti-affinity feature is turned on.
   * - ``endpoint`` = ``None``
     - (String) A new endpoint to override the endpoint in the keystone catalog.
   * - ``endpoint_type`` = ``publicURL``
     - (String) Endpoint interface in identity service to use
   * - ``insecure`` = ``False``
     - (Boolean) Disable certificate validation on SSL connections
   * - ``region_name`` = ``None``
     - (String) Region in Identity service catalog to use for communication with the OpenStack services.
   * - ``service_name`` = ``None``
     - (String) The name of the nova service in the keystone catalog
   * - **[oslo_middleware]**
     -
   * - ``enable_proxy_headers_parsing`` = ``False``
     - (Boolean) Whether the application is behind a proxy or not. This determines if the middleware should parse the headers or not.
   * - ``max_request_body_size`` = ``114688``
     - (Integer) The maximum body size for each request, in bytes.
   * - ``secure_proxy_ssl_header`` = ``X-Forwarded-Proto``
     - (String) DEPRECATED: The HTTP Header that will be used to determine what the original request protocol scheme was, even if it was hidden by a SSL termination proxy.
   * - **[task_flow]**
     -
   * - ``engine`` = ``serial``
     - (String) TaskFlow engine to use
   * - ``max_workers`` = ``5``
     - (Integer) The maximum number of workers
