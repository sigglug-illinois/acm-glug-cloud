Note: i'm assuming that hydrogen's NIC has more than one ethernet port/MAC address because it's an r720 and those were standard 4-ports IIRC.

1) We borrow a random wifi router just to have a network to install Proxmox with. Doesn't need internet access, we just need a router so that we can access the PVE web UI.

Hydrogen runs PVE (booted off a RAID-1 HDD or just one SSD). We install OPNSense as a VM on Hydrogen. Instead of passing through the NICs (which is usually a pain), we instead just create Linux Bridges on each interface and attach a corresponding NIC to the router VM. The benefit of this setup is also that if we need to migrate the router to a different physical host, as long as the interface names stay the same, we can just attach a dumb switch to the WAN connection and migrate with little to no downtime. Each linux bridge is configured to be VLAN-aware so we can setup VLANs on the managed switch as needed (treat one interface as trunk).

In OPNSense, create a few VLANS:
  a) BMC: this VLAN has no internet access and is just for accessing iDRAC, etc. BMCs are notoriously not updated and full of holes so it'd be best to restrict these as much as possible
  b) MGMT: this is where our management clients can sit, and also where the PVE GUI, etc. sits. We can give this VLAN internet access.
  c) COMPUTE: This is just where the OSes will sit.

We can then attach it as trunk to the managed switch and then configure access ports, etc. with the managed switch we have.  All the other servers just plug into the managed switch as needed.

OPNSense can also handle internal DHCP, DNS, etc. 
Note: since OPNSense is handling the WAN connection and it's NIC is virtualized, we can just give engr-it the MAC for the VM. if we ever do hardware changes, VM keeps its NIC mac and we're all good.
