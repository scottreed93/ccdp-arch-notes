# Enterprise Campus Design
## Hierarchical Network Model
Usually Cisco's network model consists of three layers - access, distribution and core. In smaller networks, a collapsed core design can combine core and distribution into a single layer.

### Hierarchy
#### Access Layer
Access layer devices provide physical connectivity to end-user devices. Access layer devices perform a number of functions including:
* Directory and Configuration Services (CDP, LLDP)
* Security Services and Network Identity and Access (802.1X, port security, DHCP snooping)
* Application Recognition Services (QoS marking, policing, queueing, DPI, NABR)
* Intelligent Network Control Services (spanning tree, IGP, LACP, BPDUGuard, Portfast etc.)
* Physical Infrastructure Services (PoE)

#### Distribution Layer
Distribution layer devices aggregate many access layer devices. Generally, each building will have a pair of distribution layer devices.
Network services should be allocated their own distribution layer.
Breaking each zone within the network up using a distribution layer allows for optimisation of routing design including IP summarisation

#### Core Layer
Core layer devices should be simple and have minimal policy or control-plane configuration

### Modularity
#### Access-Distribution Design
Three common design choices for the access-distribution block:
* **Multitier** - Based on L2 design using STP. Least flexible.
* **Virtual switch** - No need to rely on STP/FHRP. Clusters two physical switches into a virtual switch (e.g. using VSS). Can also leverage mLAG to bond access switch uplinks to a single logical uplink.
* **Routed access** - Distribution device is a router using an IGP, pushing the L2/L3 boundary down to the access switch

### Flexibility
Allows for adding new services without a major network upgrades, this supports:
* Control plane flexibility
* Forwarding plane flexibility
* User group flexibility
* Traffic management and control flexibility

#### Network Virtualisation Technologies
* **VLANs** - Can be dynamically mapped to a switchport using RADIUS attributes following a 802.1X, MAB or Webauth successful authentication
* **VRF** - Provides virtual routers with independant control planes
** **Hop-by-hop VRF-Lite** - 802.1Q trunks, SVI/Routed subinterface to VRF mappings
** **Hop-by-hop easy virtual network (EVN)**
** **Multihop GRE tunnelling** - Map each VRF to a GRE tunnel interface
** **Multihop MPLS core** - MPBGP, LDP

### Resiliency
