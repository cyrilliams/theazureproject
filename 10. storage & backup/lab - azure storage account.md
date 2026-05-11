# Configure & Manage Azure Storage Accounts

In this doc, we'll configure and manage Azure Blob Storage and File Storage Accounts.

## Create a Storage Account

First we'll search for our Storage Account:

<img width="180" height="48" alt="image" src="https://github.com/user-attachments/assets/2407e3e0-4f4b-4990-b4f7-acace9608f22" />

Create.

We'll name the Storage Account and choose the Standard option and Geo-Redundant option,
so we have our data available in the event a region/datacenter goes down.

<img width="1120" height="1056" alt="image" src="https://github.com/user-attachments/assets/c479cda7-efdf-4ee1-a3c9-b013ae61f966" />

We'll disable Public access as well:

<img width="1092" height="934" alt="image" src="https://github.com/user-attachments/assets/de31dd43-2bbb-4d1f-9541-42ae4b1a7852" />

Now we have our Storage Account. 
This can be used for Blob containers, Files Shares, Tables and Queues.

<img width="2292" height="1151" alt="image" src="https://github.com/user-attachments/assets/21a9668c-6ff7-46d0-851a-b05a843a156f" />

### Enable Access from Client IP Only

If we want to restrict access to our Storage Acccount from a specified IP,
we can go to **Security + networking > Networking > Public network access > Manage**

<img width="971" height="319" alt="image" src="https://github.com/user-attachments/assets/17ff78cd-b04e-4e63-83ca-4d68cd2345f0" />

Enable Public network access:

<img width="1738" height="270" alt="image" src="https://github.com/user-attachments/assets/fca23c83-a26d-4f36-b547-227ce369df0d" />

Configure an IPv4 or VNet.

I'll use my Public IP here:


<img width="1698" height="902" alt="image" src="https://github.com/user-attachments/assets/99030dd4-806d-4ed8-b3e0-156c4ac0e1c6" />

Save.

### Redundancy

Under **Data management > Redudancy**, we can review our Redundancy primary and secondary zones:

<img width="1624" height="1126" alt="image" src="https://github.com/user-attachments/assets/ba927ac4-19b9-42e5-bbdc-72ebb0aa035b" />

*Here we can see East US is our primary and West US is our secondary, where the Storage Account will failover to.*

### Lifecycle Management

Lifecycle management is a great way to optimize savings, as we do not want to keep every piece of data that we have in the Hot tier, especially data that we have may not use that often.

Let's create a rule to automatically configure data to be moved to the Cool tier.

Under **Data management > Lifecycle management > Add a rule**,

We'll name our Rule:

<img width="898" height="612" alt="image" src="https://github.com/user-attachments/assets/5872a86c-4d1f-47c4-a4f4-77d09f2735cf" />


Now, we will configure our Rule to automatically move data that was last modified more than 30 days ago to Cool tier storage:

<img width="974" height="624" alt="image" src="https://github.com/user-attachments/assets/aeec81c0-bed5-476f-befc-6a660d4b50c4" />

Add.

There are also a couple useful options here as well:

<img width="896" height="346" alt="image" src="https://github.com/user-attachments/assets/c71c5ab0-89d1-4e22-b779-ba6a45f32f5a" />

We can see our rule here:

<img width="2204" height="372" alt="image" src="https://github.com/user-attachments/assets/6a2b863e-15ce-4ae5-b82a-bd11adbf32e3" />

## Blob Storage

Blob storage is a great tool to use to access a file without having to go through a traditional file share or file in a directory or hard drive.

To access the file, Azure simply serves you a web url that you can access or give someone else to access, rather than having to configure setting up credentials to access a server or file share.

Lets set this up now:

Under **Data storage > Containers > Add container**








