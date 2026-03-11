# Create a V-Net Peering


##### Let's create 2 V-Net's and make sure they can communicate to each other via RDP through V-Net Peering.

Peering uses Microsoft's internal network to communicate.

We will do this using Azure Cloud Shell (bash)

#### Create Resource Group

```bash
az group create --name test-rg --location eastus2
```

<img width="1109" height="302" alt="image" src="https://github.com/user-attachments/assets/51081f66-75f1-456c-8b86-6269f9cbc11c" />

We can confirm the RG in the GUI:

<img width="1579" height="312" alt="image" src="https://github.com/user-attachments/assets/cae6814f-de47-431f-8318-baacf7bbeb28" />

#### Create V-Nets

Now we will create the V-Nets.
I'll create two of them, vnetpeer-1 and vnetpeer-2

Example command:
```bash
az network vnet create --name vnet-1 --resource-group test-rg --address-prefixes 10.0.0.0/16 --subnet-name subnet-1 --subnet-prefix 10.0.0.0/24
```

<img width="1908" height="916" alt="image" src="https://github.com/user-attachments/assets/cd241752-84f3-412c-84a2-eca1bdbbd2c7" />

#### Setup Peering

Next we will setup the peering:

I'll call it 'vnet1to2' and specify we want to peer 'Virtual network' not 'Subnet"

Next we will select the second network we want to peer to: vnetpeer-2

<img width="852" height="429" alt="image" src="https://github.com/user-attachments/assets/e0b306c2-68f6-4a88-851e-fad7abe5e6c1" />

We will fill in the rest and click 'Add'

<img width="963" height="678" alt="image" src="https://github.com/user-attachments/assets/3997d5e9-10f0-4cd9-8f38-4f79350244fe" />

Now we can see it's been created from the vnetpeer-1 side:

<img width="1329" height="324" alt="image" src="https://github.com/user-attachments/assets/4a848166-5e1e-465e-944c-d5129ebbfe76" />

As well as the vnetpeer-2 side:

<img width="1321" height="323" alt="image" src="https://github.com/user-attachments/assets/da598135-9c3f-4782-8f91-6d2e78884dfc" />


#### Test Connectivity

Let's create two VM's

<img width="771" height="774" alt="image" src="https://github.com/user-attachments/assets/1498ae3b-69d4-4e78-baf1-1bbf0bf3637d" />

*We can re-use the template to create the same specs for the VM*

<img width="852" height="641" alt="image" src="https://github.com/user-attachments/assets/e520bdcf-b087-4d5b-a7ca-de08df1668a2" />


Let's RDP in:

<img width="407" height="486" alt="image" src="https://github.com/user-attachments/assets/2e2088e2-988d-4ffd-8fbd-3d491dfae1c9" />

Let's confirm our IP with ipconfig

<img width="1421" height="791" alt="image" src="https://github.com/user-attachments/assets/6fb175cc-e270-452b-97a3-b8f9dc832193" />

Next, because of the way I have these VM's setup, lets see if we can RDP into VM2 from VM1:

In PowerShell, lets user this command:
```ps1
Test-NetConnection 10.11.1.4 -Port 3389
```

We see that because Port 3389 is open on VM2, we can hit it over 3389.

<img width="841" height="354" alt="image" src="https://github.com/user-attachments/assets/2d1d4bf8-d10c-474a-8886-ec64c216663f" />

Let's see if we can remote in:

<img width="399" height="480" alt="image" src="https://github.com/user-attachments/assets/c365dab9-3831-4b14-b7cf-c08ccdbbfc58" />

We can see that we can remote in to VM2 even though it's on a different V-Net using V-Net peering:

<img width="1294" height="773" alt="image" src="https://github.com/user-attachments/assets/a9eb56e9-a2c6-4a57-b521-be379e1c2948" />


# Test Without Peering

Let's confirm that VM2 cannot be hit if the peering is off. Let's delete it:

<img width="840" height="347" alt="image" src="https://github.com/user-attachments/assets/f1946577-f654-4421-980f-d948e0d3267e" />

Now, VM1 cannot communicate over RDP to VM2 because we ended peering:

<img width="1129" height="649" alt="image" src="https://github.com/user-attachments/assets/b9aefae0-e914-461a-a6e2-0fde9c9d0a13" />

And we can double check this by trying to connect, which we cannot:

<img width="700" height="558" alt="image" src="https://github.com/user-attachments/assets/cd471a08-22ec-4893-bd96-92db35a55a5e" />

And that's V-Net Peering.

*Originally I would like to be able to ping each of the devices. I will have to do more research in the setup of the VMs and V-Nets or NSG's as to why I could not ping VM2 from VM1. But for now, these VMs are costing me money so I will delete the whole Resource Group*

<img width="390" height="584" alt="image" src="https://github.com/user-attachments/assets/433e7354-0b67-474a-8912-243e0fc9c8e3" />
