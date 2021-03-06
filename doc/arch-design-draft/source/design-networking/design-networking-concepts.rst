===================
Networking concepts
===================

Cloud fundementally changes the ways that networking is provided and consumed.
Understanding the following concepts and decisions is imperative when making
the right architectural decisions.

OpenStack clouds generally have multiple network segments, with each
segment providing access to particular resources. The network segments
themselves also require network communication paths that should be
separated from the other networks. When designing network services for a
general purpose cloud, plan for either a physical or logical separation
of network segments used by operators and tenants. Additional network
segments can also be created for access to internal services such as the
message bus and database used by various systems. Segregating these
services onto separate networks helps to protect sensitive data and
unauthorized access.

Choose a networking service based on the requirements of your instances.
The architecture and design of your cloud will impact whether you choose
OpenStack Networking (neutron) or legacy networking (nova-network).

Networking (neutron)
~~~~~~~~~~~~~~~~~~~~

OpenStack Networking (neutron) is a first class networking service that gives
full control over creation of virtual network resources to tenants. This is
often accomplished in the form of tunneling protocols that establish
encapsulated communication paths over existing network infrastructure in order
to segment tenant traffic. This method varies depending on the specific
implementation, but some of the more common methods include tunneling over
GRE, encapsulating with VXLAN, and VLAN tags.

We recommend you design at least three network segments. The first segment
should be a public network, used to access REST APIs by tenants and operators.
The controller nodes and swift proxies are the only devices connecting to this
network segment. In some cases, this public network might also be serviced by
hardware load balancers and other network devices.

The second segment is used by administrators to manage hardware resources.
Configuration management tools also utilize this segment for deploying
software and services onto new hardware. In some cases, this network
segment is also used for internal services, including the message bus
and database services. The second segment needs to communicate with every
hardware node. Due to the highly sensitive nature of this network segment,
it needs to be secured from unauthorized access.

The third network segment is used by applications and consumers to access the
physical network, and for users to access applications. This network is
segregated from the one used to access the cloud APIs and is not capable
of communicating directly with the hardware resources in the cloud.
Communication on this network segment is required by compute resource
nodes and network gateway services that allow application data to access the
physical network from outside the cloud.

Legacy networking (nova-network)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The legacy networking (nova-network) service is primarily a layer-2 networking
service. It functions in two modes: flat networking mode and VLAN mode. In a
flat network mode, all network hardware nodes and devices throughout the cloud
are connected to a single layer-2 network segment that provides access to
application data.

However, when the network devices in the cloud support segmentation using
VLANs, legacy networking can operate in the second mode. In this design model,
each tenant within the cloud is assigned a network subnet which is mapped to
a VLAN on the physical network. It is especially important to remember that
the maximum number of VLANs that can be used within a spanning tree domain
is 4096. This places a hard limit on the amount of growth possible within the
data center. Consequently, when designing a general purpose cloud intended to
support multiple tenants, we recommend the use of legacy networking with
VLANs, and not in flat network mode.

Layer-2 architecture advantages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A network designed on layer-2 protocols has advantages over a network designed
on layer-3 protocols. In spite of the difficulties of using a bridge to perform
the network role of a router, many vendors, customers, and service providers
choose to use Ethernet in as many parts of their networks as possible. The
benefits of selecting a layer-2 design are:

* Ethernet frames contain all the essentials for networking. These include, but
  are not limited to, globally unique source addresses, globally unique
  destination addresses, and error control.

* Ethernet frames contain all the essentials for networking. These include,
  but are not limited to, globally unique source addresses, globally unique
  destination addresses, and error control.

* Ethernet frames can carry any kind of packet. Networking at layer-2 is
  independent of the layer-3 protocol.

* Adding more layers to the Ethernet frame only slows the networking process
  down. This is known as nodal processing delay.

* You can add adjunct networking features, for example class of service (CoS)
  or multicasting, to Ethernet as readily as IP networks.

* VLANs are an easy mechanism for isolating networks.

Most information starts and ends inside Ethernet frames. Today this applies
to data, voice, and video. The concept is that the network will benefit more
from the advantages of Ethernet if the transfer of information from a source
to a destination is in the form of Ethernet frames.

Although it is not a substitute for IP networking, networking at layer-2 can
be a powerful adjunct to IP networking.

Layer-2 Ethernet usage has these additional advantages over layer-3 IP network
usage:

* Speed
* Reduced overhead of the IP hierarchy.
* No need to keep track of address configuration as systems move around.

Whereas the simplicity of layer-2 protocols might work well in a data center
with hundreds of physical machines, cloud data centers have the additional
burden of needing to keep track of all virtual machine addresses and
networks. In these data centers, it is not uncommon for one physical node
to support 30-40 instances.

.. Important::

   Networking at the frame level says nothing about the presence or
   absence of IP addresses at the packet level. Almost all ports, links, and
   devices on a network of LAN switches still have IP addresses, as do all the
   source and destination hosts. There are many reasons for the continued need
   for IP addressing. The largest one is the need to manage the network. A
   device or link without an IP address is usually invisible to most
   management applications. Utilities including remote access for diagnostics,
   file transfer of configurations and software, and similar applications
   cannot run without IP addresses as well as MAC addresses.

Layer-2 architecture limitations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Layer-2 network architectures have some limitations that become noticeable when
used outside of traditional data centers.

* Number of VLANs is limited to 4096.
* The number of MACs stored in switch tables is limited.
* You must accommodate the need to maintain a set of layer-4 devices to handle
  traffic control.
* MLAG, often used for switch redundancy, is a proprietary solution that does
  not scale beyond two devices and forces vendor lock-in.
* It can be difficult to troubleshoot a network without IP addresses and ICMP.
* Configuring ARP can be complicated on a large layer-2 networks.
* All network devices need to be aware of all MACs, even instance MACs, so
  there is constant churn in MAC tables and network state changes as instances
  start and stop.
* Migrating MACs (instance migration) to different physical locations are a
  potential problem if you do not set ARP table timeouts properly.

It is important to know that layer-2 has a very limited set of network
management tools. It is difficult to control traffic as it does not have
mechanisms to manage the network or shape the traffic. Network
troubleshooting is also troublesome, in part because network devices have
no IP addresses. As a result, there is no reasonable way to check network
delay.

In a layer-2 network all devices are aware of all MACs, even those that belong
to instances. The network state information in the backbone changes whenever an
instance starts or stops. Because of this, there is far too much churn in the
MAC tables on the backbone switches.

Furthermore, on large layer-2 networks, configuring ARP learning can be
complicated. The setting for the MAC address timer on switches is critical
and, if set incorrectly, can cause significant performance problems. So when
migrating MACs to different physical locations to support instance migration,
problems may arise. As an example, the Cisco default MAC address timer is
extremely long. As such, the network information maintained in the switches
could be out of sync with the new location of the instance.

Layer-3 architecture advantages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In layer-3 networking, routing takes instance MAC and IP addresses out of the
network core, reducing state churn. The only time there would be a routing
state change is in the case of a Top of Rack (ToR) switch failure or a link
failure in the backbone itself. Other advantages of using a layer-3
architecture include:

* Layer-3 networks provide the same level of resiliency and scalability
  as the Internet.

* Controlling traffic with routing metrics is straightforward.

* You can configure layer-3 to useˇBGPˇconfederation for scalability. This
  way core routers have state proportional to the number of racks, not to the
  number of servers or instances.

* There are a variety of well tested tools, such as ICMP, to monitor and
  manage traffic.

* Layer-3 architectures enable the use of :term:`quality of service (QoS)` to
  manage network performance.

Layer-3 architecture limitations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The main limitation of layer-3 networking is that there is no built-in
isolation mechanism comparable to the VLANs in layer-2 networks. Furthermore,
the hierarchical nature of IP addresses means that an instance is on the same
subnet as its
physical host, making migration out of the subnet difficult. For these reasons,
network virtualization needs to use IPencapsulation and software at the end
hosts. This is for isolation and the separation of the addressing in the
virtual layer from the addressing in the physical layer. Other potential
disadvantages of layer 3 include the need to design an IP addressing scheme
rather than relying on the switches to keep track of the MAC addresses
automatically, and to configure the interior gateway routing protocol in the
switches.

Network design
~~~~~~~~~~~~~~

There are many reasons an OpenStack network has complex requirements. However,
one main factor is the many components that interact at different levels of the
system stack, adding complexity. Data flows are also complex. Data in an
OpenStack cloud moves both between instances across the network (also known as
East-West), as well as in and out of the system (also known as North-South).
Physical server nodes have network requirements that are independent of
instance network requirements, and must be isolated to account for
scalability. We recommend separating the networks for security purposes and
tuning performance through traffic shaping.

You must consider a number of important general technical and business factors
when planning and designing an OpenStack network. These include:

* A requirement for vendor independence. To avoid hardware or software vendor
  lock-in, the design should not rely on specific features of a vendors router
  or switch.
* A requirement to massively scale the ecosystem to support millions of end
  users.
* A requirement to support indeterminate platforms and applications.
* A requirement to design for cost efficient operations to take advantage of
  massive scale.
* A requirement to ensure that there is no single point of failure in the
  cloud ecosystem.
* A requirement for high availability architecture to meet customer SLA
  requirements.
* A requirement to be tolerant of rack level failure.
* A requirement to maximize flexibility to architect future production
  environments.

Bearing in mind these considerations, we recommend the following:

* Layer-3 designs are preferable to layer-2 architectures.
* Design a dense multi-path network core to support multi-directional
  scaling and flexibility.
* Use hierarchical addressing because it is the only viable option to scale
  network ecosystem.
* Use virtual networking to isolate instance service network traffic from the
  management and internal network traffic.
* Isolate virtual networks using encapsulation technologies.
* Use traffic shaping for performance tuning.
* Use eBGP to connect to the Internet up-link.
* Use iBGP to flatten the internal traffic on the layer-3 mesh.
* Determine the most effective configuration for block storage network.


Additional considerations
-------------------------

There are several further considerations when designing a network-focused
OpenStack cloud. Redundant networking: ToR switch high availability risk
analysis. In most cases, it is much more economical to use a single switch
with a small pool of spare switches to replace failed units than it is to
outfit an entire data center with redundant switches. Applications should
tolerate rack level outages without affecting normal operations since network
and compute resources are easily provisioned and plentiful.

Research indicates the mean time between failures (MTBF) on switches is
between 100,000 and 200,000 hours. This number is dependent on the ambient
temperature of the switch in the data center. When properly cooled and
maintained, this translates to between 11 and 22 years before failure. Even
in the worst case of poor ventilation and high ambient temperatures in the data
center, the MTBF is still 2-3 years.

Reference
https://www.garrettcom.com/techsupport/papers/ethernet_switch_reliability.pdf
for further information.

Legacy networking (nova-network)
OpenStack Networking
Simple, single agent
Complex, multiple agents
Flat or VLAN
Flat, VLAN, Overlays, L2-L3, SDN
No plug-in support
Plug-in support for 3rd parties
No multi-tier topologies
Multi-tier topologies

Preparing for the future: IPv6 support
--------------------------------------

One of the most important networking topics today is the exhaustion of
IPv4 addresses. As of late 2015, ICANN announced that the final
IPv4 address blocks have been fully assigned. Because of this, IPv6
protocol has become the future of network focused applications. IPv6
increases the address space significantly, fixes long standing issues
in the IPv4 protocol, and will become essential for network focused
applications in the future.

OpenStack Networking, when configured for it, supports IPv6. To enable
IPv6, create an IPv6 subnet in Networking and use IPv6 prefixes when
creating security groups.

Asymmetric links
----------------

When designing a network architecture, the traffic patterns of an
application heavily influence the allocation of total bandwidth and
the number of links that you use to send and receive traffic. Applications
that provide file storage for customers allocate bandwidth and links to
favor incoming traffic; whereas video streaming applications allocate
bandwidth and links to favor outgoing traffic.

Performance
-----------

It is important to analyze the applications tolerance for latency and
jitter when designing an environment to support network focused
applications. Certain applications, for example VoIP, are less tolerant
of latency and jitter. When latency and jitter are issues, certain
applications may require tuning of QoS parameters and network device
queues to ensure that they queue for transmit immediately or guarantee
minimum bandwidth. Since OpenStack currently does not support these functions,
consider carefully your selected network plug-in.

The location of a service may also impact the application or consumer
experience. If an application serves differing content to different users,
it must properly direct connections to those specific locations. Where
appropriate, use a multi-site installation for these situations.

You can implement networking in two separate ways. Legacy networking
(nova-network) provides a flat DHCP network with a single broadcast domain.
This implementation does not support tenant isolation networks or advanced
plug-ins, but it is currently the only way to implement a distributed
layer-3 (L3) agent using the multi host configuration. OpenStack Networking
(neutron) is the official networking implementation and provides a pluggable
architecture that supports a large variety of network methods. Some of these
include a layer-2 only provider network model, external device plug-ins, or
even OpenFlow controllers.

Networking at large scales becomes a set of boundary questions. The
determination of how large a layer-2 domain must be is based on the
amount of nodes within the domain and the amount of broadcast traffic
that passes between instances. Breaking layer-2 boundaries may require
the implementation of overlay networks and tunnels. This decision is a
balancing act between the need for a smaller overhead or a need for a smaller
domain.

When selecting network devices, be aware that making a decision based on the
greatest port density often comes with a drawback. Aggregation switches and
routers have not all kept pace with Top of Rack switches and may induce
bottlenecks on north-south traffic. As a result, it may be possible for
massive amounts of downstream network utilization to impact upstream network
devices, impacting service to the cloud. Since OpenStack does not currently
provide a mechanism for traffic shaping or rate limiting, it is necessary to
implement these features at the network hardware level.

Tunable networking components
-----------------------------

Consider configurable networking components related to an OpenStack
architecture design when designing for network intensive workloads
that include MTU and QoS. Some workloads require a larger MTU than normal
due to the transfer of large blocks of data. When providing network
service for applications such as video streaming or storage replication,
we recommend that you configure both OpenStack hardware nodes and the
supporting network equipment for jumbo frames where possible. This
allows for better use of available bandwidth. Configure jumbo frames across the
complete path the packets traverse. If one network component is not capable of
handling jumbo frames then the entire path reverts to the default MTU.

:term:`Quality of Service (QoS)` also has a great impact on network intensive
workloads as it provides instant service to packets which have a higher
priority due to the impact of poor network performance. In applications such as
Voice over IP (VoIP), differentiated services code points are a near
requirement for proper operation. You can also use QoS in the opposite
direction for mixed workloads to prevent low priority but high bandwidth
applications, for example backup services, video conferencing, or file sharing,
from blocking bandwidth that is needed for the proper operation of other
workloads. It is possible to tag file storage traffic as a lower class, such as
best effort or scavenger, to allow the higher priority traffic through. In
cases where regions within a cloud might be geographically distributed it may
also be necessary to plan accordingly to implement WAN optimization to combat
latency or packet loss

Network hardware selection
~~~~~~~~~~~~~~~~~~~~~~~~~~

The network architecture determines which network hardware will be
used. Networking software is determined by the selected networking
hardware.

There are more subtle design impacts that need to be considered. The
selection of certain networking hardware (and the networking software)
affects the management tools that can be used. There are exceptions to
this; the rise of *open* networking software that supports a range of
networking hardware means there are instances where the relationship
between networking hardware and networking software are not as tightly
defined.

For a compute-focus architecture, we recommend designing the network
architecture using a scalable network model that makes it easy to add
capacity and bandwidth. A good example of such a model is the leaf-spline
model. In this type of network design, you can add additional
bandwidth as well as scale out to additional racks of gear. It is important to
select network hardware that supports port count, port speed, and
port density while allowing for future growth as workload demands
increase. In the network architecture, it is also important to evaluate
where to provide redundancy.

Some of the key considerations in the selection of networking hardware
include:

Port count
 The design will require networking hardware that has the requisite
 port count.

Port density
 The network design will be affected by the physical space that is
 required to provide the requisite port count. A higher port density
 is preferred, as it leaves more rack space for compute or storage
 components. This can also lead into considerations about fault domains
 and power density. Higher density switches are more expensive, therefore
 it is important not to over design the network.

Port speed
 The networking hardware must support the proposed network speed, for
 example: 1 GbE, 10 GbE, or 40 GbE (or even 100 GbE).

Redundancy
 User requirements for high availability and cost considerations
 influence the level of network hardware redundancy.
 Network redundancy can be achieved by adding redundant power
 supplies or paired switches.

 .. note::

    Hardware must support network redundacy.

Power requirements
 Ensure that the physical data center provides the necessary power
 for the selected network hardware.

 .. note::

    This is not an issue for top of rack (ToR) switches. This may be an issue
    for spine switches in a leaf and spine fabric, or end of row (EoR)
    switches.

Protocol support
 It is possible to gain more performance out of a single storage
 system by using specialized network technologies such as RDMA, SRP,
 iSER and SCST. The specifics for using these technologies is beyond
 the scope of this book.

There is no single best practice architecture for the networking
hardware supporting an OpenStack cloud. Some of the key factors that will
have a major influence on selection of networking hardware include:

Connectivity
 All nodes within an OpenStack cloud require network connectivity. In
 some cases, nodes require access to more than one network segment.
 The design must encompass sufficient network capacity and bandwidth
 to ensure that all communications within the cloud, both north-south
 and east-west traffic have sufficient resources available.

Scalability
 The network design should encompass a physical and logical network
 design that can be easily expanded upon. Network hardware should
 offer the appropriate types of interfaces and speeds that are
 required by the hardware nodes.

Availability
 To ensure access to nodes within the cloud is not interrupted,
 we recommend that the network architecture identify any single
 points of failure and provide some level of redundancy or fault
 tolerance. The network infrastructure often involves use of
 networking protocols such as LACP, VRRP or others to achieve a highly
 available network connection. It is also important to consider the
 networking implications on API availability. We recommend a load balancing
 solution is designed within the network architecture to ensure that the APIs,
 and potentially other services in the cloud are highly available.

Networking software selection
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

OpenStack Networking (neutron) provides a wide variety of networking
services for instances. There are many additional networking software
packages that can be useful when managing OpenStack components. Some
examples include:

* Software to provide load balancing

* Network redundancy protocols

* Routing daemons

Some of these software packages are described in more detail in the
`OpenStack network nodes chapter <http://docs.openstack.org/ha-guide
/networking-ha.html>`_ in the OpenStack High Availability Guide.

For a general purpose OpenStack cloud, the OpenStack infrastructure
components need to be highly available. If the design does not include
hardware load balancing, networking software packages like HAProxy will
need to be included.

For a compute-focused OpenStack cloud, the OpenStack infrastructure
components must be highly available. If the design does not include
hardware load balancing, you must add networking software packages, for
example, HAProxy.
