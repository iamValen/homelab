
> ISC is the most updated DHCP server option in OPNsense up to this date

1. Enable ISC DHCP for each wanted interface
2. Configure:
	- Subnet: Network Address
	- Subnet Mask: Desired Mask
	- Define IP Range
3. After applying all correct setting it's important to verify if there's no other DHCP server enabled for the desired interface.