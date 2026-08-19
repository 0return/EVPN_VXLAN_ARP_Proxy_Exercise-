                                                     ARP-Proxy

Enable ARP-Proxy to reduce the amount of broadcasted ARP messages.
By default, an L2 EVPN service behaves like a regular L2 network -- All BUM traffic is flooded to all possible destinations, including the remote VXLAN VTEPs.
This becomes a scaling issue, if more VTEPs are added, more BUM traffic will be flooded.
ARP-Proxy is a feature to manage how ARP requests are handled by a VTEP

Topology:

<img width="989" height="329" alt="image" src="https://github.com/user-attachments/assets/1fcc1393-f91d-4224-820f-ff5e46ff986e" />
