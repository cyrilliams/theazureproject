# Project: Enterprise Hybrid Infrastructure in Azure

In this project, we'll build a small enterprise environment that resembles a real companies architecture.

## Goals

We'll create a hybrid environment that uses a Hub and Spoke topology for networking, Entra ID Connect from my on Prem Windows Server, 
as well as Azure services like Azure Files, Application Gateway, Azure Monitor, Azure Backup & Site Recovery, and RBAC.

## Create Resource Group

First, I'll create a Resource Group to manage and put all of our resources into:

<img width="821" height="425" alt="image" src="https://github.com/user-attachments/assets/42194000-8365-4520-8707-dc495d69fe01" />


## Create Networks

<img width="92" height="97" alt="image" src="https://github.com/user-attachments/assets/052067c2-b2c3-4c36-bf0f-d657e1fe57b4" />

*I changed the RG to the correct RG after*

After, let's creat our Hub and Spoke V-Nets.

### Hub V-Net

We'll start with the Hub, which will represent the main branch/core location.

<img width="801" height="691" alt="image" src="https://github.com/user-attachments/assets/ccf73368-1f92-4190-be94-63dc6d40f4e9" />

We'll use the 10.0.0.0/16 address space.

We'll then create 3 subnets: GatewaySubnet, Management and SharedServices. Each will use the 10.0.0.0/24 address space.

<img width="824" height="728" alt="image" src="https://github.com/user-attachments/assets/767c419a-f404-4757-90c5-ccdd406bc696" />

We'll create and move to a Spoke V-Net

### Spoke V-Net

Next, we'll create our next V-Net. This will be modeled after a sub-location:

<img width="838" height="612" alt="image" src="https://github.com/user-attachments/assets/44197630-b346-47e3-8349-0df85168df34" />

We'll give it a 10.1.0.0/16 address space and two Subnets: Web and Application:

<img width="735" height="599" alt="image" src="https://github.com/user-attachments/assets/21dd110b-3b79-44c0-9d5a-06530168c486" />

### Implement Connectivity with V-Net Peering

We want these two V-Nets to talk to each other. Let's enable peering between the two.

Let's go to our Main Location V-Net, **Settings > Peerings > Add**

<img width="844" height="766" alt="image" src="https://github.com/user-attachments/assets/9d77c485-be43-4e8e-9fd0-a2709f863eb8" />

Now, if we go into our Lake Worth V-Net, we can see Peering has been enabled as well:

<img width="1330" height="679" alt="image" src="https://github.com/user-attachments/assets/1c9ddce8-75ea-466d-9ff8-d91040ab3128" />



### Create an Azure Virtual Machine

Lets create an Azure Linux VM in our Application Subnet.

<img width="789" height="675" alt="image" src="https://github.com/user-attachments/assets/9103893c-d7e1-4cf8-9590-79c7fb42b50d" />

<img width="862" height="670" alt="image" src="https://github.com/user-attachments/assets/867e5748-527c-44fb-9d96-d70968d35977" />

We'll allow SSH and create an SSH Key:

<img width="797" height="675" alt="image" src="https://github.com/user-attachments/assets/04a680ad-2fd0-4a21-b364-f957733f87ae" />

We'll configure this to be in our Applications Subnet in our Lake Worth VNet.

We'll block public access. We want internal traffic to this Machine only:

<img width="874" height="641" alt="image" src="https://github.com/user-attachments/assets/96396efc-ac5a-40b1-98c7-eb3768e00984" />

Next, we'll download our Key Pair and create our VM.

Now we can see our new VM with No Public IP:

<img width="1904" height="862" alt="image" src="https://github.com/user-attachments/assets/c03b927b-204c-4472-a27d-0c9143decdf2" />








## Implement Site (Point) to Site Connectivity

We'll use a VPN to connect our on Prem Windows Server to be able to talk to our Azure Machine and services. We'll use a Point to Site VPN because I only have one machine.

### Create Gateway

First, we'll create a VPN Gateway. We'll go to **Connections > VPN gateway > VPN gateways > Add**

We'll use the GatewaySubnet from our mainLocation Vnet:

<img width="788" height="747" alt="image" src="https://github.com/user-attachments/assets/10572e83-027c-449e-8ec0-dc4363571998" />

We'll create two Public IPs as well:

<img width="812" height="617" alt="image" src="https://github.com/user-attachments/assets/2599750f-dedb-49b5-b2b6-e23a131d8ee0" />

After several minutes, our Gateway is deployed.

### Set Up Point to Site Gateway

In our newly created Gateway, go to **Settings > Point to site configuration > Configure now**

We'll give it an address pool, Auth type and a public IP:

<img width="1895" height="730" alt="image" src="https://github.com/user-attachments/assets/61670698-9980-4ebc-9f37-024aa9c86161" />

We'll set up our Tenant, Audience and Issuer, using our Tenant ID:

<img width="739" height="410" alt="image" src="https://github.com/user-attachments/assets/b05d4b08-bea0-4058-a1bb-497593f71ce4" />

Next, on our On-Prem Windows Server, we'll download the VPN client configuration file:

<img width="855" height="196" alt="image" src="https://github.com/user-attachments/assets/be2bb6a5-7f51-417f-a8a0-377e76579986" />


<img width="781" height="168" alt="image" src="https://github.com/user-attachments/assets/d6ff6a41-36ec-448a-9d8a-950cdfa20202" />


<img width="1920" height="934" alt="image" src="https://github.com/user-attachments/assets/f53462f9-e95a-438f-9eb4-19e2390a229a" />

Next, we'll donwload the actual VPN client:

<img width="1920" height="934" alt="image" src="https://github.com/user-attachments/assets/fb881210-46b8-4dff-adc9-2f1ac1814f01" />

In the VPN client zip folder, we'll run the Install Powershell script:

<img width="1920" height="934" alt="image" src="https://github.com/user-attachments/assets/6fc9927f-5f08-4a56-833c-412f89f3eafb" />

Open the Azure VPN Client and import the Point to Site Client Config from earlier:

<img width="1920" height="934" alt="image" src="https://github.com/user-attachments/assets/e21c8f35-1410-4c11-87c5-66c004dd2e31" />

It populates the configuration:

<img width="1920" height="934" alt="image" src="https://github.com/user-attachments/assets/728b0756-07a3-47c8-a981-d8d01b256f9c" />

Save and connect:

<img width="1920" height="934" alt="image" src="https://github.com/user-attachments/assets/7b038a5c-4f2a-409b-838d-ea5407d0bdc5" />

### Troubleshooting the VPN Connection: App Permissions

We are met with this error that says we must have 'Sign in and read user profile permissions'

<img width="1033" height="219" alt="image" src="https://github.com/user-attachments/assets/0653ffc8-066b-4a79-aacf-fb7ce4a0c4fa" />

After looking into, we need to give permissions to Azure VPN in Entra.

Go to **Entra ID > Enterprise Applications > Azure VPN > Security > Permissions**

<img width="1637" height="422" alt="image" src="https://github.com/user-attachments/assets/5e798278-3dfe-422a-992e-49d2e304e456" />

Next, we'll click 'Grant admin consent'

<img width="1364" height="217" alt="image" src="https://github.com/user-attachments/assets/bf450fa5-35a2-47a3-a90b-e01e00f7a9f1" />

<img width="1060" height="788" alt="image" src="https://github.com/user-attachments/assets/befa8f4b-104c-4b3d-842a-5abaa48f6d20" />

Now we can see the correct permissions:

<img width="1373" height="642" alt="image" src="https://github.com/user-attachments/assets/d7f695c0-76f8-4361-a46c-0b5208665f51" />

Lets try to connect to the VPN again:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/48d98500-fd82-4e5e-97ce-a566bf00e2df" />

After some trial and error with changing the the config, we are in!

We can see our config here as well:

<img width="567" height="278" alt="image" src="https://github.com/user-attachments/assets/6200deef-5062-4093-b75e-fa0baab1de5e" />



## Configure Network

Now, we need to configure our Vnet to allow traffic from our on Prem device.

### Modify Peering

On both our VNet Peers, we'll check the following options:

<img width="783" height="775" alt="image" src="https://github.com/user-attachments/assets/5775daa4-8b54-427b-a3f8-0f4c4ae4dc9c" />

On the Spoke Vnet Peer, we'll make sure it can use the Hub's Gateway:

<img width="898" height="868" alt="image" src="https://github.com/user-attachments/assets/0f13dff7-ee53-498e-8ffc-fa5beedc1735" />


### Re-Download VPN Client and Verify

Redownload the P2S VPN config files and connect. Let's try pinging our Linux VM, located in our Lake Worth Vnet, in the Applications Subnet:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/3ccec345-53d7-4050-afe7-3746514e2ec6" />

Amazing!

Let's try to SSH into our internal Linux VM:

<img width="992" height="941" alt="image" src="https://github.com/user-attachments/assets/caccdee1-4621-494e-ac1f-70adacde3ea4" />

Hooray!

#### Verify External Access

On my PC (not on the Windows VM I am testing with), let's try to ping the Linux VM

<img width="1113" height="626" alt="image" src="https://github.com/user-attachments/assets/7524b7fa-ef69-425a-90e4-375dfa5caf65" />

Failed! This is what we want! No out bound access!



## Enable Backup

<img width="111" height="99" alt="image" src="https://github.com/user-attachments/assets/ece5608b-cf89-4ef7-807d-7dd123bf4678" />

Let's say our Linux VM was extremely important and could tolerate no downtime, let's setup a Recovery Services Vault to enable Active Site Recovery in case of a datacenter issue.

### Create Recovery Service Vault

First, we'll create the Recovery Service Vault (RSV) in the same region as the VM.

<img width="754" height="572" alt="image" src="https://github.com/user-attachments/assets/582a06c9-8a89-49c1-b0c5-c9dfbb23ab72" />

We'll enable Geo-Redudancy to make sure our VM is available in another Region:

<img width="731" height="136" alt="image" src="https://github.com/user-attachments/assets/a37e8f96-2fda-4afa-8b6e-569c95f9b219" />

Create.

After that is done, we'll go to our VM, **Backup + disaster recovery > Backup**

<img width="1373" height="654" alt="image" src="https://github.com/user-attachments/assets/95a91372-376b-46ed-af7f-dee4eef6f33a" />

We'll keep the default Backup Policy

<img width="614" height="566" alt="image" src="https://github.com/user-attachments/assets/a4339097-7fee-421c-b6e0-df56bbf1c0bd" />

Enable backup.

<img width="1910" height="470" alt="image" src="https://github.com/user-attachments/assets/103b9ace-abcc-4fec-8a1f-b17df801c3ce" />

Now we can see our VM is backed up with the Backup Policy of every 4 hours.

<img width="567" height="302" alt="image" src="https://github.com/user-attachments/assets/506cf718-2544-4b2b-9e18-79b512f7b587" />








## Connect On Premises Windows Server and Connect Identity

For this part, we'll connect our on Prem Windows Server running Active Directory to our Azure tenant.

Here we have created an OU called Lake Worth, but have no members in it. Let's add a member named "Billy Bob", who is a Manager.

<img width="1440" height="900" alt="image" src="https://github.com/user-attachments/assets/658c5c74-8f2e-4e74-b448-d915dbc00c3d" />

Next, let's donwload the Azure Connect agent from Entra ID, under **Entra ID > Entra Connect**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/701e4aec-9a6f-44fd-8e51-be3048798ee4" />

We'll sign in and go through the prompts:

<img width="920" height="652" alt="image" src="https://github.com/user-attachments/assets/b5b99553-694b-4c1f-a291-875e8de4976d" />

Enter our on Prem admin credentials:

<img width="911" height="652" alt="image" src="https://github.com/user-attachments/assets/1f1e03b7-814a-45f9-9bfb-4c457f0ed5bd" />

Install:

<img width="937" height="664" alt="image" src="https://github.com/user-attachments/assets/56eac812-d0e8-4b28-a3ed-eefacb874a1b" />

After a couple minutes, we can see Billy Bob is in our Entra ID, with 'On-premises syncronization' set to 'Yes'

<img width="1630" height="451" alt="image" src="https://github.com/user-attachments/assets/307c0238-fa5e-4054-a71e-027bc2bb4feb" />






## Storage Account/Azure File Sync with AD Authentication

Next, lets create a Storage Account to sync with our on Prem File Share and verify that Billy Bob can access the file share.


### Create Storage Account

<img width="113" height="98" alt="image" src="https://github.com/user-attachments/assets/c88b7fbe-b271-4591-9730-e9040a94c8ad" />

Lets create our Storage Account here:

<img width="818" height="762" alt="image" src="https://github.com/user-attachments/assets/e81a53af-dc68-458d-a062-464fb2269b16" />

Let's secure access by limiting access to our Vnet:

<img width="788" height="777" alt="image" src="https://github.com/user-attachments/assets/00780c57-9d2b-453a-806c-51ab4fe9eeb0" />

After, I'll create a Classic File Share:

<img width="794" height="660" alt="image" src="https://github.com/user-attachments/assets/1365b7cc-24e8-473a-a27e-a63ae5404a11" />

I'll also enable Backups with our RSV:

<img width="800" height="459" alt="image" src="https://github.com/user-attachments/assets/4127cdba-40cc-4f5d-b06c-d85dd22ac755" />


### Create File Sync

We'll create an On Prem File Sync.

<img width="106" height="99" alt="image" src="https://github.com/user-attachments/assets/19c10e2e-756a-4c81-bbb4-b3400b3abdb6" />

Go to **File Sync > Create**

<img width="769" height="541" alt="image" src="https://github.com/user-attachments/assets/55f21618-ec98-4262-b6d4-dd6a4adad916" />

Once deployed, go to **Sync Groups > Create**, and link our Storage Account and File Share:

<img width="725" height="437" alt="image" src="https://github.com/user-attachments/assets/01855e95-8a25-4b0f-8bf4-238a7f144cf4" />

On our Server, we'll download and install the Azure File Sync Agent:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7f6d5a15-68ef-41dd-a129-428f0aa2c82f" />

Run and configure the sync:

<img width="1708" height="960" alt="image" src="https://github.com/user-attachments/assets/95cf3b88-fb59-4423-b3ae-6287f42f58d9" />

Now we can refresh our Registered Servers and see our on-prem Server:

<img width="2551" height="603" alt="image" src="https://github.com/user-attachments/assets/b05c3020-5c91-485b-8b7a-aced9987c88e" />

We'll now copy the Share from on on-prem Server to use as a Server Endpoint

<img width="2549" height="1225" alt="image" src="https://github.com/user-attachments/assets/877697c3-2cda-4284-b3ec-63e3ed159d30" />



















