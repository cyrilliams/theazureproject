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

If we want to restrict access to our Storage Account from a specified IP,
we can go to **Security + networking > Networking > Public network access > Manage**

<img width="971" height="319" alt="image" src="https://github.com/user-attachments/assets/17ff78cd-b04e-4e63-83ca-4d68cd2345f0" />

Enable Public network access:

<img width="1738" height="270" alt="image" src="https://github.com/user-attachments/assets/fca23c83-a26d-4f36-b547-227ce369df0d" />

Configure an IPv4 or VNet.

I'll use my Public IP here:


<img width="1698" height="902" alt="image" src="https://github.com/user-attachments/assets/99030dd4-806d-4ed8-b3e0-156c4ac0e1c6" />

Save.

### Redundancy

Under **Data management > Redundancy**, we can review our Redundancy primary and secondary zones:

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

<img width="531" height="454" alt="image" src="https://github.com/user-attachments/assets/57cc7e91-9ddb-4771-a942-920053737f7f" />

Create.

### Immutable Blob Storage

To make sure the Blob Container stays in an immutable state, we'll click the '...' on our Blob, 
then **Access Policy > Immutable blob storage > Add policy**

We'll change to 'Time-based retention' and set the retention period to 180 days:

<img width="720" height="507" alt="image" src="https://github.com/user-attachments/assets/c20f0bed-78b5-43ca-8abe-15951fdf3259" />

Save.

This will keep data from being deleted for that set duration.

## Manage Blob Container

We'll first upload a file into our Blob Container.

We'll click our Storage account, then click Upload.

We can upload a file here:

<img width="714" height="336" alt="image" src="https://github.com/user-attachments/assets/b2e80cb5-907c-488d-84b2-cb5ecc85fb94" />

And we have Advanced options to go along with the upload, such as Access tier, upload folder, and the retention policy (if we did not set it earlier)

<img width="712" height="852" alt="image" src="https://github.com/user-attachments/assets/21553711-6cb5-452c-9f4f-e941286f2ef1" />


Upload a file and click Upload.

We can see that it uploaded our file and created a Directory. I set this in the Upload folder (not shown in the last picture)

<img width="2215" height="379" alt="image" src="https://github.com/user-attachments/assets/59b25c79-01a5-4ab5-befc-bb7ca5410f79" />


Now, we can see our file and it's info:

<img width="2207" height="396" alt="image" src="https://github.com/user-attachments/assets/49f9c815-44ef-4252-be0b-11f46ad8d8b6" />



We can click the file and get the URL:

<img width="1383" height="1116" alt="image" src="https://github.com/user-attachments/assets/825d6428-741e-44a1-9f41-db21552987bf" />

Let's copy and paste it in our browser:

<img width="1498" height="360" alt="image" src="https://github.com/user-attachments/assets/dea00d62-eefd-400f-aaa5-45f1936f0873" />

We get this error stating that public access is not permitted. Let's change this.

### Configure Limited Access

We'll configure limited access using a Shared Access Signature

We'll right click our file and click the '...', then click 'Generate SAS'

<img width="228" height="588" alt="image" src="https://github.com/user-attachments/assets/b62827e7-76d2-41e4-ac70-95bac03b011b" />


This allows us to configure and set the Policies around what type of access is given and for how long:

<img width="715" height="959" alt="image" src="https://github.com/user-attachments/assets/4c53ee53-3870-4751-a3da-39694e7b59bf" />

We'll click 'Generate SAS token and URL'

It gives us our Token and URL here:

<img width="716" height="168" alt="image" src="https://github.com/user-attachments/assets/37bd5887-368d-4524-838e-54000a3be4dc" />



Now, if we enter that URL into our browser:

<img width="2560" height="1380" alt="image" src="https://github.com/user-attachments/assets/e25fa2ea-c35a-4160-8e58-b45c24515245" />

BOOM, we now have access!

## Manage File Storage

Next, we'll create an Azure File share.

We'll go to our Storage Account, **Data storage > File shares > + File shares**

We'll give it a name:

<img width="984" height="335" alt="image" src="https://github.com/user-attachments/assets/cd4f2226-5e91-4a5f-be64-a91d1f3128ba" />


We can see that it uses Port 445, like a regular file share:

<img width="904" height="86" alt="image" src="https://github.com/user-attachments/assets/0ae374dd-90e9-4642-8fdc-9ed6163d78fe" />

Create the file share.

*There should be a section to review the Access tier but it did not show up for me this time*

Now we have a file share:

<img width="2542" height="1140" alt="image" src="https://github.com/user-attachments/assets/3a3f8954-b9b0-411c-a136-912bc1c8eaf9" />


I'll upload a picture using the Upload button:

<img width="720" height="607" alt="image" src="https://github.com/user-attachments/assets/95e00991-7c88-4e7b-b779-7e30ef5ac3df" />

If we click 'Browse', we can find our newly uploaded file:

<img width="2540" height="370" alt="image" src="https://github.com/user-attachments/assets/006d6587-f876-45f7-a561-1c31c91fa6fc" />

### Restrict Network Access

We may want to restrict who can access our file share. Lets do that by creating a VNet.

<img width="262" height="64" alt="image" src="https://github.com/user-attachments/assets/381c5c63-aa80-43e2-95cd-233514ed58ba" />

In the new VNet, we'll go to **Settings > Service endpoints > Add**, and configure the following Microsoft.Storage service endpoint:

<img width="535" height="556" alt="image" src="https://github.com/user-attachments/assets/b968628d-6cb8-4b46-8017-b0f3ea7b56f0" />

Add.

We'll go back to our Storage Account and go to 
**Security + networking > Networking > Public network access > Manage**

Under Virtual Networks, we'll add an existing VNet:

<img width="851" height="254" alt="image" src="https://github.com/user-attachments/assets/095c7b1a-31d7-4339-9217-3750120f3e8d" />

Select the appropriate Vnet and Subnet:

<img width="362" height="344" alt="image" src="https://github.com/user-attachments/assets/b0d08c0d-8964-4551-8d83-bd8a00adbb39" />


We can see it's been added:

<img width="2539" height="284" alt="image" src="https://github.com/user-attachments/assets/dd3932be-75b4-458f-b9f4-8473b9e2bba1" />

*For this test, we'll delete my machines public IP address so we can verify we cannot access the file*

Save.

Now if we go to **Storage browser > File shares**, and select our file, we get this error:

<img width="1192" height="711" alt="image" src="https://github.com/user-attachments/assets/4e3cc8e2-5a35-4ace-b80a-146fcb8a2867" />

*We can see that we are no longer authorized to perform this operation and it even recommends adding our IP address*

If we add our (Public) IP address back and retry, we are now able to access the file:

<img width="1715" height="615" alt="image" src="https://github.com/user-attachments/assets/e94d41a1-c45b-490a-b329-8ff9efaa5904" />

Now we have access to our file:

<img width="2555" height="1176" alt="image" src="https://github.com/user-attachments/assets/7bc3cb21-5be2-4e6a-b093-a6013942eb31" />
