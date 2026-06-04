# Data and Storage Replication and Redundancy

In this lab, we'll go over configuring Data & Storage Replication and Redundancy.

Our objectives will be to:
- Change our Storage Account from Zone Redundant Storage (ZRS) to Geo Redundant Storage (GRS) and/or Read Access Geo Redundant Storage.
- Enable Object Replication between Storage Accounts in different Regions.

# Data & Storage Redundancy

## Create Storage Account

We'll create a storage account in East US 2. We'll use ZRS that way our data is spread across 3 different datacenters in a Zone.

<img width="1024" height="793" alt="image" src="https://github.com/user-attachments/assets/b9d9a528-19f0-4f70-84dd-33abcf394edd" />

After deployment, go to the Storage Account, **Data management > Redundancy**

We can see that our Zone is West US 2

<img width="1274" height="833" alt="image" src="https://github.com/user-attachments/assets/a9318eec-42de-47e9-abfa-52a53c9bbb08" />

## Change Redundancy

I'll create a Container and upload a file in there:

<img width="1908" height="381" alt="image" src="https://github.com/user-attachments/assets/69a53582-36bb-4605-9fb6-97fd025e336d" />

Let's change our Storage Account Redundancy settings by going back to **Data management > Redundancy > Redundancy**

Change from ZRS to GZRS and Save.

<img width="1010" height="241" alt="image" src="https://github.com/user-attachments/assets/252ba1ba-95dd-4de6-8b8e-1b094d06a912" />

After many hours, it finally updates and shows us our Secondary Region:

<img width="1102" height="588" alt="image" src="https://github.com/user-attachments/assets/56d1be1c-a384-43b2-9fc2-d05fe6f36706" />

We can also look at the Storage Endpoints, and see that there is only a Primary endpoint.
That is because data is being written to both Regions.

<img width="574" height="431" alt="image" src="https://github.com/user-attachments/assets/5784eed1-e77c-486b-8c8a-7e73f4fb958d" />

## Change to Read Only Geo Redundant Storage

*I had to create another Storage Account for this part due to Redundancy change limitations*

In this Storage Account, we can see that it is set to ZRS and only has one Primary endpoint.

<img width="1910" height="466" alt="image" src="https://github.com/user-attachments/assets/ab1006dd-0ba9-4ebb-80a6-0c16c30a87ea" />

Let's change this from ZRS to RA-GRS.

After saving, we can see that we now have a Secondary Endpoint for all of our Storage services:

<img width="1902" height="780" alt="image" src="https://github.com/user-attachments/assets/1a317af0-a943-4f34-a5cf-44a61af1cd79" />










---

# Object Replication

Let's create a new Storage Account to replicate our data to. Let's put it in a separate region:

<img width="819" height="767" alt="image" src="https://github.com/user-attachments/assets/8ef983ab-20ee-420c-af05-1be3e11ab439" />


This will be the account we want data to get replicated to.

In our Source Storage Account, we'll enable Versioning.

Go to **Data management > Data protection > Tracking > Enable versioning for blobs**

<img width="1349" height="764" alt="image" src="https://github.com/user-attachments/assets/b01a9108-62ca-434e-a7d6-9c4e2972ef25" />

Repeat for the Destination Storage Account:


## Create Replication Rule

Under our Source Storage Account, we'll go to **Data management > Object replication > Create replication rules**

We'll select our Destination Storage Account (cyrilaz104datarep2) and Destination Blob Container (testcontainer2) and Create.

<img width="1203" height="665" alt="image" src="https://github.com/user-attachments/assets/90e929d4-eaa9-4a01-bc4f-7d3c65bec7ea" />


Currently, I have nothing in both Storage Accounts:

<img width="1917" height="1032" alt="image" src="https://github.com/user-attachments/assets/e26c4c2e-6aad-4e15-9c33-33ac029b09c7" />


Let's upload something to our Source Storage Account.

<img width="947" height="420" alt="image" src="https://github.com/user-attachments/assets/b511830c-21ad-4793-881a-38a342e4e572" />

After a couple seconds, we can see that it is automatically replicated to our Destination Storage Account:

<img width="1911" height="541" alt="image" src="https://github.com/user-attachments/assets/26b46fe2-e2d7-4e8c-8c68-a157ce17d0d7" />

If we try uploading something to the Destination, we get an error because we are not allowed to upload to a Replicated Storage Container.

<img width="288" height="162" alt="image" src="https://github.com/user-attachments/assets/8d7f6e38-7a45-4968-bf1c-ec9dfa864a85" />


Let's try uploading to the Source one more time:

<img width="1905" height="490" alt="image" src="https://github.com/user-attachments/assets/86ba60a6-23bf-49c6-afd1-831c2fa17d6c" />

After a couple seconds, it yet again replicates:

<img width="1904" height="446" alt="image" src="https://github.com/user-attachments/assets/a075c89c-8fac-44f8-b6a6-39138fa1bd94" />




