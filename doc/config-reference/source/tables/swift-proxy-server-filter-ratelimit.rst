..
  Warning: Do not edit this file. It is automatically generated and your
  changes will be overwritten. The tool to do so lives in the
  openstack-doc-tools repository.

.. list-table:: Description of configuration options for ``[filter-ratelimit]`` in ``proxy-server.conf``
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - ``account_blacklist`` = ``c,d``
     - Comma separated lists of account names that will not be allowed. Returns a 497 response. r: for containers of size x, limit requests per second to r. Will limit PUT, DELETE, and POST requests to /a/c/o. container_listing_ratelimit_x = r: for containers of size x, limit listing requests per second to r. Will limit GET requests to /a/c.
   * - ``account_ratelimit`` = ``0``
     - If set, will limit PUT and DELETE requests to /account_name/container_name. Number is in requests per second.
   * - ``account_whitelist`` = ``a,b``
     - Comma separated lists of account names that will not be rate limited.
   * - ``clock_accuracy`` = ``1000``
     - Represents how accurate the proxy servers' system clocks are with each other. 1000 means that all the proxies' clock are accurate to each other within 1 millisecond. No ratelimit should be higher than the clock accuracy.
   * - ``container_listing_ratelimit_0`` = ``100``
     -  with container_listing_ratelimit_x = r, for containers of size x, limit container GET (listing) requests per second to r. The container rate will be linearly interpolated from the values given. With the default values, a container of size 5 will get a rate of 75.
   * - ``container_listing_ratelimit_10`` = ``50``
     -  with container_listing_ratelimit_x = r, for containers of size x, limit container GET (listing) requests per second to r. The container rate will be linearly interpolated from the values given. With the default values, a container of size 5 will get a rate of 75.
   * - ``container_listing_ratelimit_50`` = ``20``
     -  with container_listing_ratelimit_x = r, for containers of size x, limit container GET (listing) requests per second to r. The container rate will be linearly interpolated from the values given. With the default values, a container of size 5 will get a rate of 75.
   * - ``container_ratelimit_0`` = ``100``
     -  with container_ratelimit_x = r, for containers of size x, limit write requests per second to r. The container rate will be linearly interpolated from the values given. With the default values, a container of size 5 will get a rate of 75.
   * - ``container_ratelimit_10`` = ``50``
     -  with container_ratelimit_x = r, for containers of size x, limit write requests per second to r. The container rate will be linearly interpolated from the values given. With the default values, a container of size 5 will get a rate of 75.
   * - ``container_ratelimit_50`` = ``20``
     -  with container_ratelimit_x = r, for containers of size x, limit write requests per second to r. The container rate will be linearly interpolated from the values given. With the default values, a container of size 5 will get a rate of 75.
   * - ``log_sleep_time_seconds`` = ``0``
     - To allow visibility into rate limiting set this value > 0 and all sleeps greater than the number will be logged.
   * - ``max_sleep_time_seconds`` = ``60``
     - App will immediately return a 498 response if the necessary sleep time ever exceeds the given max_sleep_time_seconds.
   * - ``rate_buffer_seconds`` = ``5``
     - Number of seconds the rate counter can drop and be allowed to catch up (at a faster than listed rate). A larger number will result in larger spikes in rate but better average accuracy.
   * - ``set log_address`` = ``/dev/log``
     - Location where syslog sends the logs to.
   * - ``set log_facility`` = ``LOG_LOCAL0``
     - Syslog log facility.
   * - ``set log_headers`` = ``false``
     - If True, log headers in each request.
   * - ``set log_level`` = ``INFO``
     - Log level.
   * - ``set log_name`` = ``ratelimit``
     - Label to use when logging.
   * - ``use`` = ``egg:swift#ratelimit``
     - Entry point of paste.deploy in the server.
