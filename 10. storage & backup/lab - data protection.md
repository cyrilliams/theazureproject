# Data Protection

In this lab, we'll create a VM, create a Recovery Service vault and a backup policy for the VM, 
as well as use VM replication.

## Recovery Services Vault

We'll start by using a Recovery Services Vault. 
This is a service that allows us to create back ups of VM, files and databases,
as well as utilize replication for Resources.

We'll find our Recovery Services vault:

<img width="238" height="48" alt="image" src="https://github.com/user-attachments/assets/4a23e8e6-7c70-4e34-ad3c-0b34dd385367" />

Create a Vault:

<img width="1046" height="816" alt="image" src="https://github.com/user-attachments/assets/24044593-8fae-4805-808e-6c6fbe5bc51c" />

Under the RS Vault, we'll go to **Settings > Properties > Backup Configuration > Update**

<img width="1442" height="1099" alt="image" src="https://github.com/user-attachments/assets/dfa5360a-179f-4cc0-9783-f6686e9dcd79" />

We'll select our desire level of Redundancy:

<img width="712" height="722" alt="image" src="https://github.com/user-attachments/assets/d93cb52e-bfd5-4569-ab82-150f8e6a5be9" />

## Configure VM Backup

Under the RS Vault, go to **Overview > Backup**

<img width="1882" height="424" alt="image" src="https://github.com/user-attachments/assets/4be7a64f-0535-463f-9f22-a70b8e5f267c" />

We'll configure our backup, select the Policy type, and select the VM we would like to Backup:

*Its important to note the different Policy types*

<img width="2538" height="1082" alt="image" src="https://github.com/user-attachments/assets/d41e3fa7-9601-4265-bf6f-24386bba69d7" />

###  Create Policy

We'll create a new policy here:

<img width="816" height="79" alt="image" src="https://github.com/user-attachments/assets/f213a637-d49a-4840-bd5a-cca5ec76a22e" />

We can change when the backups take place and the frequency, as well as retention time:

<img width="1048" height="478" alt="image" src="https://github.com/user-attachments/assets/91f3fe7a-46df-428b-881c-02fe1f6e0518" />

Enable backup.

Now if we go to the RS Vault, **Protected items > Backup items > Azure Virtual Machine**,
you can see the newly backed up VM:

<img width="2530" height="504" alt="image" src="https://github.com/user-attachments/assets/42008037-85de-471d-a05c-a9de73626b08" />


## Monitor Azure Backup

We will use a storage account to be a repository for Azure Monitoring Logs & Analytics

Let's create the Storage Account by searching for it:

We'll create a Blob Storage Account:

<img width="1202" height="1107" alt="image" src="https://github.com/user-attachments/assets/60b8dcf3-970b-49a7-a233-00e34f46b6c3" />


We'll go back to our RS Vault, go to **Monitoring > Diagnostic settings > Add a diagnostic setting**

<img width="658" height="518" alt="image" src="https://github.com/user-attachments/assets/11b56dca-7685-403b-9186-e5b7447d0b58" />


We'll name the Diagnostic Settings and select which Logs we want to send:

<img width="1358" height="1080" alt="image" src="https://github.com/user-attachments/assets/17b94d2b-5253-45a0-94f3-f540997ddc77" />

Under 'Destination details', we'll select our Blob Storage Account:

<img width="736" height="704" alt="image" src="https://github.com/user-attachments/assets/3d36cfb1-655c-43f8-acc0-4e21ee760cb7" />

Save.

We'll go back to our RS Vault, **Monitoring > Backup Jobs**

We can see our Backup Job and confirm that it's saving to our Blob Storage Account.

<img width="1428" height="960" alt="image" src="https://github.com/user-attachments/assets/4dd46740-9197-4bdf-9f0b-8ae74c21df70" />

If we can go to our Blob Storage Account, we can see there are newly created Containers for the Logs:

<img width="1960" height="396" alt="image" src="https://github.com/user-attachments/assets/45b541ef-4ab2-4acc-b8d7-a1c6fc76650d" />


## Enable Replication

We'll create another Recovery Services Vault by searching for it.

We'll name it differently and put it in a separate Resource Group and Region.

*This is important because in a real scenario, we want our Resources to go to a different region incase the region or datacenter(s)
the Resource is in goes down*

<img width="960" height="727" alt="image" src="https://github.com/user-attachments/assets/af345e3c-6f63-4daf-9e11-0548a3ed05c7" />


We'll go to our VM and go to **Backup + disaster recovery > Disaster recovery

We'll select our Target Region:

<img width="1492" height="850" alt="image" src="https://github.com/user-attachments/assets/1252d3b5-e0e1-44f0-b4ed-a67965cae688" />

We can see the Source and Target info on the 'Advanced settings' tab:

<img width="1132" height="1050" alt="image" src="https://github.com/user-attachments/assets/9fe56da2-c394-47a5-9c17-30c95a6efa9c" />

We'll also have to create an Automation Account, which is used to run automation tools like PowerShell and Python scripts.

<img width="1120" height="188" alt="image" src="https://github.com/user-attachments/assets/705be35c-b3a4-443e-8e4f-647ef250911f" />

Start Replication. *This will take a while*

Now if we go under our Region 2 RS Vault, **Protected items > Replicated items**, 
we can see our VM is currently being replicated

<img width="1558" height="791" alt="image" src="https://github.com/user-attachments/assets/c1008c9f-8fd3-4222-b968-01c816e7c82c" />

*We can also test failover here*

We also get a visual graph of how our VM is replicated:

<img width="1690" height="1012" alt="image" src="https://github.com/user-attachments/assets/d89d7241-d486-4936-9d60-d5e5526da811" />

