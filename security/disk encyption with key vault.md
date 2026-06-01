# Disk Encryption with Azure Key Vault

In this doc, we'll encyrpt an Azure Virtual Disk with a Key Encryption Key (KEK) stored in Azure Key Vault

## Create Resources

We'll create our Resource Group (RG) and add the following:
- A virtual machine
- Azure Key Vault

<img width="1823" height="828" alt="image" src="https://github.com/user-attachments/assets/f2123025-d972-462c-915e-5eb8512d2781" />

## Enable Disk Encryption

Under our Key Vault, we'll go to **Settings > Access configuration > Resource access** and select Azure Disk Encryption (ADE)

<img width="2543" height="857" alt="image" src="https://github.com/user-attachments/assets/35742daa-11a9-465e-9669-4cfafdc3bc66" />

*If this doesn't work, you may have to enable a Firewall bypass:*

<img width="1932" height="530" alt="image" src="https://github.com/user-attachments/assets/9cda821a-3ee8-40a3-8c00-7eece7f3fd72" />

## Create Key Encryption Key (KEK)

Next, we'll go to our Key Vault, **Objects > Keys > Generate/Import**

<img width="2183" height="1037" alt="image" src="https://github.com/user-attachments/assets/4a369e39-bd9c-4298-b3d3-11b2c890a563" />

## Configure Access Policies

Next, we'll go to Access Policies and Create an Access Policy

For this Key, we want it to only be able to Wrap (Encrypy) and Unwrap (Decrypt) the Disk:

<img width="1156" height="1080" alt="image" src="https://github.com/user-attachments/assets/3cb69b13-07ea-4de5-b46e-0c88c342559d" />

Under Principal, we'll select 'Azure Key Vault'

<img width="1103" height="977" alt="image" src="https://github.com/user-attachments/assets/ee51cdfa-e4dc-4776-80fa-b2bb04e3cb12" />


### Enable Disk Encryption

Now on our VM disk, we'll enable Disk Encyrption.

Under our Virtual Machine, we'll go to **Settings > Disks > Additional settings**, and select the OS Disk, Key Vault & Key:

<img width="977" height="539" alt="image" src="https://github.com/user-attachments/assets/cce1b58b-db0d-4331-a397-6d6e77099e59" />

Save. *This may take a while*



