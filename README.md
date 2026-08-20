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


Spine1 and Spine2 capture the VXLAN packets.

<img width="1611" height="315" alt="image" src="https://github.com/user-attachments/assets/6986fd99-9cd2-4e80-ac34-ba279ce6f863" />

You can add "verbose" in the command for more details

<img width="827" height="819" alt="image" src="https://github.com/user-attachments/assets/ed0dce8a-e48c-40cf-b6ce-13e37677a457" />


Now that an ARP request for an existing IP address.

Customer100-1

<img width="444" height="146" alt="image" src="https://github.com/user-attachments/assets/20185820-f1a0-46af-a9a8-afeb793b369e" />


Customer100-2

<img width="718" height="196" alt="image" src="https://github.com/user-attachments/assets/4b29f873-92ea-4321-957e-21268b28bf58" />


Spine1


<img width="1594" height="243" alt="image" src="https://github.com/user-attachments/assets/94462605-814f-4567-8710-98bc0f7f894a" />


You can check the ARP table on Customer100-1

<img width="417" height="94" alt="image" src="https://github.com/user-attachments/assets/97f96b88-a3c1-4aa4-af9a-c3d505c6d0cd" />


SR Linux supports proxy-ARP on L2 EVPN service. SR Linux will then intercept incoming ARP requests and directly reply to them instead of flooding the request to all other VTEPs

Config


<img width="525" height="215" alt="image" src="https://github.com/user-attachments/assets/08a799cd-a6a8-4efb-930d-5aeb4026a6fd" />


An immediate effect to enabling proxy/ARP is that a new entry is added to the MAC table

<img width="1300" height="375" alt="image" src="https://github.com/user-attachments/assets/71721524-4450-47fa-b5a4-abfa3ff1d486" />

The system adds a "reserved" destination with a system chassis MAC address (show platform chassis).


On Customer100-1 generate a Gratuitous ARP, this typically performed by applications to notify a neighbor of their own MAC and IP address. In fact a gARP is an unsolicited ARP reply populated with its own MAC/IP address.

<img width="352" height="92" alt="image" src="https://github.com/user-attachments/assets/6a9750b7-363a-4e73-a309-1041119a1fcd" />


Leaf1 learn Customer1-100´s MAC address

<img width="1304" height="386" alt="image" src="https://github.com/user-attachments/assets/e3fb5631-fed2-4a8d-8f80-e0e05dc83cc8" />







