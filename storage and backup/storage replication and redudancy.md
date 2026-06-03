# Data and Storage Replication and Redudancy

In this lab, we'll go over configuring Data & Storage Replication and Redudancy.

Our objectives will be to:
- Change our Storage Account from Zone Redundant Storage (ZRS) to Geo Redudnact Storage (GRS) and/or Read Access Geo Redundant Storage.
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


















---

# Object Replication

Let's create a new Storage Account to replicate our data to. Let's put it in a seperate region:

<img width="819" height="767" alt="image" src="https://github.com/user-attachments/assets/8ef983ab-20ee-420c-af05-1be3e11ab439" />





