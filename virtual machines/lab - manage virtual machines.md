# Managing Azure Virtual Machines

In this lab, we will deploy Azure Virtual Machines, Virtual Machine Scale Sets, and manage VM's using PowerShell and Bash.

## Create Virtual Machine (Portal)

First, we'll create our Virtual Machines:

<img width="106" height="127" alt="image" src="https://github.com/user-attachments/assets/56fb3511-262c-4240-9cf7-681f7aad25b3" />

We'll start by selecting Zones 1 & 2. 
This will create two different machines that we can name individually:

<img width="1420" height="791" alt="image" src="https://github.com/user-attachments/assets/545adea6-7f32-4cb3-a939-523f69384639" />

We'll configure our VM's with the following options:

<img width="1059" height="856" alt="image" src="https://github.com/user-attachments/assets/57b6b40b-24ff-4452-88fd-148bef8c4948" />

Under Disks, we'll leave the defaults:

<img width="1176" height="880" alt="image" src="https://github.com/user-attachments/assets/9a5a810f-e38a-45a1-8a6c-bba53c29bc79" />

For Networking, we'll let Azure create our Vnet and Subnet:

<img width="1058" height="756" alt="image" src="https://github.com/user-attachments/assets/20b2c369-d22d-47aa-8fd5-6c3bbc152bca" />

We'll disable 'Boot diagnostics' under 'Management', then Review and Create.

## Scale Virtual Machine

In the real world, we may need to scale up or Virtual Machine so it has more resources, 
whether RAM or CPU power, it may need to be scaled.

Lets do this now:

Go to our VM, and go to **Availability + scale > Size**

We'll select another VM SKU and click Resize:

<img width="2220" height="1092" alt="image" src="https://github.com/user-attachments/assets/ea60bf7c-3158-459b-b6d4-8685dc4b939b" />

This will restart the VM and change the resources the VM has.

### Add Storage Space

To add Storage space via a Storage Disk, we'll go to **Settings > Disks > Create and attach a new disk**

Choose your configuration and apply!

<img width="2538" height="648" alt="image" src="https://github.com/user-attachments/assets/f9afbbe1-c31d-4eea-88e5-7536086ca16c" />

If we change our mind and want to increase the size or change the type of Disk, 
we can go to the Disk, go to **Settings > Size + performance**, and chose to increase either options.


I'll change to a Standard SSD with 64GBs of Storage:

<img width="2547" height="960" alt="image" src="https://github.com/user-attachments/assets/5d76153b-0b56-4986-a215-b8e4c4fe1433" />

*You will need to stop the VM first to do this*

And now verify the type and size has changed:

<img width="1939" height="444" alt="image" src="https://github.com/user-attachments/assets/0f45119f-cb11-456c-96f4-a55851628310" />

## Deploy Virtual Machine Scale Sets

<img width="279" height="54" alt="image" src="https://github.com/user-attachments/assets/2d1efde3-91c0-4de0-8189-0ef10c1d90fb" />

Let's now create a VM Scale Set, for when we need to scale our VM's automatically when resource needs increase.

Click Create.

We'll start off by Deploying to 3 different Zones, 
as well as choosing Uniform Orchestration mode, for identical VMs.

<img width="1018" height="1092" alt="image" src="https://github.com/user-attachments/assets/2ae05bd1-8113-43cc-bf36-44a8382c21f7" />

We'll choose our Scaling mode and instance count:

<img width="1010" height="986" alt="image" src="https://github.com/user-attachments/assets/02ac84b9-3ae6-447d-a49e-1c029db14009" />

We'll skip the Spot and Disks tab.

Under Networking, we'll create our Vnet and Subnet:

<img width="956" height="579" alt="image" src="https://github.com/user-attachments/assets/c0e0c8e9-c7a6-4cde-819b-ca9593c9d456" />


To create a Network Security Group (NSG) from this part of the Scale Set setup, 
we'll click the Edit or pencil icon on the created NIC for the VM Scale Set:

<img width="1018" height="271" alt="image" src="https://github.com/user-attachments/assets/1f3932e7-dcb0-4864-bb59-945e1308e3d4" />

Click 'Create new'

<img width="990" height="700" alt="image" src="https://github.com/user-attachments/assets/8ec42a1e-f2ce-4462-b223-de07293a7b8e" />


We'll create an inbound rule to allows HTTP traffic:

<img width="2556" height="382" alt="image" src="https://github.com/user-attachments/assets/f21ba438-08cb-4128-8d5c-a210f3b42762" />

Under Load Balancing, we'll use the Azure Load Balancer and quickly create one:

<img width="980" height="452" alt="image" src="https://github.com/user-attachments/assets/e411c171-0e70-40d1-80b7-1ce6596454a8" />

We'll Review + Create.

## Scale Out the VM Scale Set

Now lets configure scaling out or Scale Set

### Scale Out

Now in our VM Scale Set, we'll go to **Availability + scale > Scaling > Custom autoscale**

<img width="1176" height="772" alt="image" src="https://github.com/user-attachments/assets/dc25ed8d-296c-40bc-9709-4861a683b26e" />


We'll create a rule that scales out our Scale Set if the CPU reaches 75% over a 5 minute period:

<img width="723" height="1098" alt="image" src="https://github.com/user-attachments/assets/32703d8e-4bef-4dc2-99f4-333ef1b859ea" />


### Scale In

We may want to scale our Scale Set in when we have less demand. 
Lets configure this:

We'll add a Rule to decrease our VM's by 50% if CPU percentage is less than 20%:

<img width="727" height="1099" alt="image" src="https://github.com/user-attachments/assets/1c1171a6-d603-421f-915c-2b86fa48317b" />

Our Scaling Rules now look like this:

<img width="1152" height="851" alt="image" src="https://github.com/user-attachments/assets/5f728a8b-bed0-465f-a453-4173ed66eabc" />

Great for when demand increases and decreases. 

### Instance Limits

Instance Limits are also great to keep a minimum and maximum amount of VM instances available:

<img width="1091" height="83" alt="image" src="https://github.com/user-attachments/assets/373f0914-a3bc-4be1-b2b2-ed55097ab966" />

Save.


## Create a Virtual Machines via Azure Cloud

Now we'll create a VM using Azure Cloud. First we'll start with PowerShell.

### PowerShell.

In our Cloud Shell, we'll run:
```
New-AzVm -ResourceGroupName 'az104vmdemo-rg' -Name 'azvm01' -Location "East US" -Image 'Win2019Datacenter' -Zone '2' -Size 'Standard_D2s_v3' -Credential (Get-Credential)
```
Press Enter:

*Put the admin creds of the VM not your admin creds*

<img width="2068" height="376" alt="image" src="https://github.com/user-attachments/assets/f9df5e2e-f890-4e55-8fa7-9a78f08e3df2" />


Now we get this:

<img width="1630" height="428" alt="image" src="https://github.com/user-attachments/assets/1ca6bba1-e946-4029-9523-5561583c8dac" />

```
ResourceGroupName        : az104vmdemo-rg                                                                               
Id                       : /subscriptions/[subscription-id]/resourceGroups/az104vmdemo-rg/providers/Microsoft.Compute/virtualMachines/azvm01
VmId                     : 453a7788-0170-4517-80f1-f0b56fdc82f5                                                         
Name                     : azvm01                                                                                       
Type                     : Microsoft.Compute/virtualMachines                                                            
Location                 : eastus                                                                                       
Tags                     : {}                                                                                           
HardwareProfile          : {VmSize}                                                                                     
NetworkProfile           : {NetworkInterfaces}                                                                          
OSProfile                : {ComputerName, AdminUsername, WindowsConfiguration, Secrets, AllowExtensionOperations, RequireGuestProvisionSignal}
ProvisioningState        : Succeeded                                                                                    
StorageProfile           : {ImageReference, OsDisk, DataDisks, AlignRegionalDisksToVMZone}                              
Zones                    : {2}                                                                                          
FullyQualifiedDomainName : azvm01-0442ea.East US.cloudapp.azure.com                                                     
TimeCreated              : 5/16/2026 7:58:01 PM                                                                         
Etag                     : "2"                                                                                          
```
Now if we run ```get-azVM -ResourceGroupName 'az104vmdemo-rg' -Status```, 
we get the VM's in our Resource Group and the status:

<img width="1166" height="131" alt="image" src="https://github.com/user-attachments/assets/ff5cc3b7-2af8-4b48-9aa8-ac301a4b0606" />


Let's do it again with Bash:

## Bash

We'll run:
```
az vm create --name azvm02 --resource-group az104vmdemo-rg --image Win2019Datacenter --admin-username cyriladmin --generate-ssh-keys --size Standard_D2s_v3
```

<img width="1718" height="151" alt="image" src="https://github.com/user-attachments/assets/062a8bd0-b33c-48d3-9859-de18f6f84b47" />

Enter.

Now we get:
```
{
  "fqdns": "",
  "id": "/subscriptions/5a8ee2f3-c30e-4ee4-b5ba-446f5ccdb7ae/resourceGroups/az104vmdemo-rg/providers/Microsoft.Compute/virtualMachines/azvm02",
  "location": "eastus",
  "macAddress": "7C-ED-8D-D6-98-B2",
  "powerState": "VM running",
  "privateIpAddress": "10.1.0.6",
  "publicIpAddress": "104.45.206.230",
  "resourceGroup": "az104vmdemo-rg"
}
```

To verify the specifications of our new VM, run:

```az vm show 
cyril [ ~ ]$ az vm show --resource-group az104vmdemo-rg --name azvm02
```
And we get this:
```
{
  "etag": "\"2\"",
  "hardwareProfile": {
    "vmSize": "Standard_D2s_v3"
  },
  "id": "/subscriptions/[subscription-id/resourceGroups/az104vmdemo-rg/providers/Microsoft.Compute/virtualMachines/azvm02",
  "location": "eastus",
  "name": "azvm02",
  "networkProfile": {
    "networkInterfaces": [
      {
        "id": "/subscriptions/[subscription-id/resourceGroups/az104vmdemo-rg/providers/Microsoft.Network/networkInterfaces/azvm02VMNic",
        "resourceGroup": "az104vmdemo-rg"
      }
    ]
  },
  "osProfile": {
    "adminUsername": "cyriladmin",
    "allowExtensionOperations": true,
    "computerName": "azvm02",
    "requireGuestProvisionSignal": true,
    "secrets": [],
    "windowsConfiguration": {
      "enableAutomaticUpdates": true,
      "enableVMAgentPlatformUpdates": true,
      "patchSettings": {
        "assessmentMode": "ImageDefault",
        "patchMode": "AutomaticByOS"
      },
      "provisionVMAgent": true
    }
  },
  "provisioningState": "Succeeded",
  "resourceGroup": "az104vmdemo-rg",
  "storageProfile": {
    "dataDisks": [],
    "diskControllerType": "SCSI",
    "imageReference": {
      "exactVersion": "17763.8755.260509",
      "offer": "WindowsServer",
      "publisher": "MicrosoftWindowsServer",
      "sku": "2019-datacenter-gensecond",
      "version": "latest"
    },
    "osDisk": {
      "caching": "ReadWrite",
      "createOption": "FromImage",
      "deleteOption": "Detach",
      "diskSizeGB": 127,
      "managedDisk": {
        "id": "/subscriptions/[subscription-id/resourceGroups/az104vmdemo-rg/providers/Microsoft.Compute/disks/azvm02_disk1_f25c89a1bd08424aa646378199d7b788",
        "resourceGroup": "az104vmdemo-rg",
        "storageAccountType": "Premium_LRS"
      },
      "name": "azvm02_disk1_f25c89a1bd08424aa646378199d7b788",
      "osType": "Windows"
    }
  },
  "tags": {},
  "timeCreated": "2026-05-16T20:16:05.3581016+00:00",
  "type": "Microsoft.Compute/virtualMachines",
  "vmId": "41ce935c-41c9-435c-b396-b45b6e8c483e"
}
```

### Verify in Portal

If we go to our Virtual Machines tab in Azure, we can see our newly created VM's:

<img width="2543" height="503" alt="image" src="https://github.com/user-attachments/assets/54f027d6-d7dc-48c0-aa7c-6b6bbb169e96" />


### Delete Resource Group

Lets delete the Resource Group using CLI:

```
cyril [ ~ ]$ az group delete --name az104vmdemo-rg 
Are you sure you want to perform this operation? (y/n): y
```

After a bit of waiting, our RG is deleted:

<img width="1815" height="912" alt="image" src="https://github.com/user-attachments/assets/fbbeac3f-025d-4bac-828d-a25da94093ce" />

