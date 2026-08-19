                                                     ARP-Proxy

Enable ARP-Proxy to reduce the amount of broadcasted ARP messages.
By default, an L2 EVPN service behaves like a regular L2 network -- All BUM traffic is flooded to all possible destinations, including the remote VXLAN VTEPs.
This becomes a scaling issue, if more VTEPs are added, more BUM traffic will be flooded.
ARP-Proxy is a feature to manage how ARP requests are handled by a VTEP

Topology:

<img width="989" height="329" alt="image" src="https://github.com/user-attachments/assets/1fcc1393-f91d-4224-820f-ff5e46ff986e" />


When a host needs to reach another Host or Router, it will broadcast an ARP request to learn the L2 MAC address of that remote Host/Router.
You can verify by using the Linux "arping" command on Customer100-1

<img width="376" height="93" alt="image" src="https://github.com/user-attachments/assets/7fc671f6-49b2-482f-aacd-4086afb0df74" />

This will generatre ARP broadcast request for the non-existing 192.168.100.254 IP address for 3 seconds

At the same time, connect onto Customer100-2 or Customer100-3 and use tcpdump, they receive the broadcast ARP request

<img width="731" height="126" alt="image" src="https://github.com/user-attachments/assets/99f2a42d-e924-4658-8210-b5f592989579" />
