It is possible that some ISP's routers Wi-Fi still works in bridge mode, so you don't actually need to have a seperate AP.

#### <span style="color:rgb(255, 0, 0)">Important</span>
This is not recommended if it's not documented by the ISP, in my case it wasn't but it worked very well. To make sure it works it's **important to check a couple things**.

Before doing this you should have completed [[OpnSense Basic Setup]]
# Setup
OPNsense is connected to the ISP through the WAN port, but since it's a WAN port it can't flow traffic from the OPNsense to the IPS, which is needed because we want all Wi-Fi devices to be **behind** the OPNsense Firewall. 
To solve this connect the ISP also through a LAN port, directly to the machine or to a switch connected to the LAN machine.

At this point check in the ISP router web interface if:
- DHCP is OFF
- Firewall is OFF
- Wi-Fi is ON

