# Creating a Network Security Groups (NSG)

NSG's are important to allow or deny certain rules in or out of your network, 
similar to how Firewalls allow and deny traffic.

Now we will configure our NSG by creating one. 
I'll create one to match our V-Net

<img width="954" height="456" alt="image" src="https://github.com/user-attachments/assets/180e0bc7-b4bc-4d6a-ab32-f28e5b471610" />

I won't do too much here for now, but I'll block inbound traffic for RDP (Port 3389). 
This would be beneficial if we only used something like Azure Bastion, which uses HTTPS traffic and does not use port 3389 to connect to Virtual Machines.

<img width="714" height="1156" alt="image" src="https://github.com/user-attachments/assets/e1fddccf-f9a6-4d1b-a2ba-7901228ce97b" />

### Priority Numbers

NSG's also feature Priority Numbers.
These tell the NSG which rules are higher or lower in priority and tell the NSG which needs to be processed first.

Here, I have block RDP with a priority of 500. 
I'll also block insecure web traffic with a priority of 400.

The NSG will process/look at the HTTP deny rule first and then go to the deny RDP rule, then all other rules:

<img width="1473" height="258" alt="image" src="https://github.com/user-attachments/assets/00f47bae-2441-4e4d-937f-a8b6e0906913" />


You can apply NSG rules to subnets and virtual NIC's.
