# Implement Site Connectivity

In this doc, we'll connect two segmented VNets and establish connectivity between them.

## Create Environment


I have an Resource Group that includes:
```
2 VNets with
  2 Subnets in each VNet
  Application Security Group
  Network Security Group  
Public and Private DNS Zones
```
<img width="1320" height="580" alt="image" src="https://github.com/user-attachments/assets/579ad6d7-73c9-4a5a-9792-9cd983111914" />

We'll need to add two Virtual Machines, one in each VNet.

### Create Virtual Machines

We'll start with our first VM that will reside in our CoreServicesVnet

<img width="1158" height="757" alt="image" src="https://github.com/user-attachments/assets/90e8d885-bdb9-406a-a8a3-2943262f64ba" />

We'll use the default disk.

Go to Networking and select the correct VNet and Subnet:

<img width="893" height="641" alt="image" src="https://github.com/user-attachments/assets/cd93de5f-5a60-4e8f-9939-51edf1eb7b4b" />

We'll create the second Virtual Machine and link it to the other VNet

<img width="936" height="644" alt="image" src="https://github.com/user-attachments/assets/118d4f73-064a-40b2-9e5a-ffde4c8080d0" />


## Test Network Connectivity

We'll use the 'Network Watcher' tool to test connectivity.

<img width="97" height="97" alt="image" src="https://github.com/user-attachments/assets/8bb6a0a4-2334-4e2a-a491-01d0ef7cbccd" />

From the Network Watcher tab, we'll go to **Network diagnostics tool >  Connection troubleshoot**

<img width="266" height="575" alt="image" src="https://github.com/user-attachments/assets/cc7af277-3fa8-4dc6-be32-3facabeafd57" />

Select our Virtual Machines and select Port 3389 over TCP:

<img width="999" height="767" alt="image" src="https://github.com/user-attachments/assets/30c05590-db7d-4c25-a1de-d74a68442ceb" />

We'll run our Diagnostic Test:

<img width="977" height="436" alt="image" src="https://github.com/user-attachments/assets/3d3694f3-8628-402c-963e-163ae244d652" />

We can see it's failed. This is what we are expecting because we do not have connectivity set up within our VNets! Let's fix that.


## Set Up VNet Peering

We'll use VNet Peering to establish a connection between our VNets.

Let's go to our CoreServicesVnet, then go to **Settings > Peering > Add**

### Remote Virtual Peer:

We'll select our other VNet select Allow 'ManufacturingVnet' to access 'CoreServicesVnet & Allow 'ManufacturingVnet' to receive forwarded traffic from 'CoreServicesVnet'.

Make sure we select Virtual Network and not Subnet peering.

<img width="890" height="668" alt="image" src="https://github.com/user-attachments/assets/32436ff2-28d9-4272-a52d-a3eb6431a118" />

### Local Virtual Peer:

We'll name and select Allow 'CoreServicesVnet' to access 'ManufacturingVnet' & Allow 'CoreServicesVnet' to receive forwarded traffic from 'ManufacturingVnet'

<img width="787" height="421" alt="image" src="https://github.com/user-attachments/assets/024e7927-492d-4d1a-a05f-425cee04c654" />

Add.

### Verify Peering

We can see our Peering is set up on our CoreServicesVnet:

<img width="1910" height="350" alt="image" src="https://github.com/user-attachments/assets/379365f6-c121-4372-9568-efdcdb909844" />

Let's check our ManufacturingVnet:

<img width="1901" height="354" alt="image" src="https://github.com/user-attachments/assets/4ad0e6b2-fdb2-4ae0-b7b3-7c7d52966f08" />

Now that we see both of our VNet, let's test connectivity.

<img width="382" height="382" alt="image" src="https://github.com/user-attachments/assets/59006189-967a-40dd-9f9d-d2fcac095839" />


## Test Connectivity Between Virtual Machines


Let's first grab the private IP of our CoreServicesVM. We'll go to the VM, **Networking > Network settings > Private IP Address**

*This one is 10.20.30.4 (because I put it in the Core Subnet with an address space of 10.20.30.0/24)*

<img width="1483" height="427" alt="image" src="https://github.com/user-attachments/assets/40d1de46-5874-4001-934f-9a02850abdc5" />

Now we'll go over to the ManufacturingVM, **Operations > Run command > RunPowerShellScript**

We'll enter ```Test-NetConnection 10.20.30.4 -Port 3389``` and Run.

After a couple seconds, our Output is:

<img width="321" height="149" alt="image" src="https://github.com/user-attachments/assets/7a065293-a1a3-4a7a-95b1-8cf343a6acb6" />

```
ComputerName     : 10.20.30.4
RemoteAddress    : 10.20.30.4
RemotePort       : 3389
InterfaceAlias   : Ethernet
SourceAddress    : 10.30.30.4
TcpTestSucceeded : True
```


Nice!

### Test with Network Watcher

Let's set up Network Watch to test connectivity between our VMs.

Go to **Network Watcher > Network diagnostic tools > Connection troubleshoot**

Select our Virtual Machines and specify Port 3389


<img width="996" height="767" alt="image" src="https://github.com/user-attachments/assets/8b7d2958-307a-49a6-94ba-7495fc3cea57" />

Run.

Now we can see all tests have succeeded:

<img width="968" height="411" alt="image" src="https://github.com/user-attachments/assets/4915dfc7-1ce6-4fa9-b56a-5420b0adff24" />


## Create Custom Route

We'll create a subnet to configure traffic from the Perimeter of our CoreServicesVnet and our other internal subnets in the CoreServicesVnet.

<img width="834" height="436" alt="image" src="https://github.com/user-attachments/assets/67275e70-5ecc-4dbb-a9b2-89b6a5b6e387" />

We'll use the Route Tables tool.

<img width="112" height="95" alt="image" src="https://github.com/user-attachments/assets/5166ad39-1c17-4084-99a2-86daaccdbd62" />

Create.

<img width="759" height="580" alt="image" src="https://github.com/user-attachments/assets/9c0c505c-839b-44d6-8fda-2cd7ca512368" />

Review and Create.

After the Route Table has been created, we'll go to **Settings > Routes > Add**

We'll specify the following:

Destination type: We'll put the address range of our CoreServicesVnet

Next hop type: Virtual appliance + IP of our virtual appliance *(this could be a firewall or packet inspection appliance)*


<img width="1910" height="498" alt="image" src="https://github.com/user-attachments/assets/187cd3ff-be09-401f-b8eb-33587ab30770" />


This type of setup would be extremely useful if we had a DMZ (Demilitarized Zone) where we want traffic inspected before entering our internal network. 

### Example Scenario

You host a public web server in the perimeter subnet.

Users access:

https://company.com

The web server needs to talk to:

internal database servers
Active Directory
backend APIs

Security team does NOT want:

``Web Server → Internal Network directly``

Instead they require:

``Web Server → Firewall/NVA → Internal Network``

So the firewall can:
inspect packets,
block attacks,
monitor traffic,
enforce rules.

