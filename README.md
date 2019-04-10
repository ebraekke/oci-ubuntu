# oci-ubuntu

ansible scripts for Ubuntu 18.X VMs in the Oracle OCI Cloud. 
They may very well work for earlier releases of Ubuntu as well, 
but I have not tested.

This simple suite demonstrates how to "inject" the correct `iptables`
rules to allow for other services than ssh. 

Oracle will create a set of `iptables` chains at the launch of a new VM.
These are needed for (among other things) to ensure that only sudo users can 
muck with iscsi (block storage). 

The documentation clearly states that `ufw` cannot be used to define your own 
rules. This is different than for Centos7 and Oracle Linux 7 where you can 
use `firewall-cmd`. So the only way to allow for additional services on your
Ubuntu VM is to add your rules correctly into the chain. You can of course
solve this by removing the `REJECT` line in the `INPUT` chain, 
but I would not recommend doing so. The Oracle documentation, at least, does 
not suggest this is an option.

Also note that since a firewall definition exists on the VM it is **not**
sufficient to change the security list on your Virtual Cloud Network or 
subnet(s).

