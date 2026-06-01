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

## Troubleshooting

When encrypting the Disk, I ran in to this error:

<img width="685" height="466" alt="image" src="https://github.com/user-attachments/assets/944571be-81c9-4db6-88e4-d955cab587fe" />

If we look closely, we can see that because we are running Windows Server 2022, we need to use RSA 3072.
I had chosen RSA 2048.

Let's create a new version of our Key:

We'll go back to our Key and create a new version using RSA 3072 or higher:

<img width="1989" height="957" alt="image" src="https://github.com/user-attachments/assets/4a341ce6-47d7-4da1-9cc0-e5a7828cc308" />

Now we can see both of our Key versions:

<img width="1153" height="480" alt="image" src="https://github.com/user-attachments/assets/32739259-6820-4071-9973-c7cdb5613077" />

### Retry Encryption

Let's try encrypting the Disk again!

<img width="935" height="173" alt="image" src="https://github.com/user-attachments/assets/ba82dbd2-8e83-4aae-9999-31722a6e15b9" />

We can see it gives us the option for the Current or Older version. Select the Current and Save.

Now we can see our Encryption instance:

<img width="2545" height="870" alt="image" src="https://github.com/user-attachments/assets/2b8fc58a-07a1-4988-a8dc-c89072643d0d" />


## Verify Encryption

Let's verify our disk was Encrypted.

If we go back to our VM,  **Settings > Disks**, we can see our disk has now shows it is Encrypted:

<img width="2548" height="689" alt="image" src="https://github.com/user-attachments/assets/ae1f84e2-d0b3-4624-814f-0c1c94231f05" />

Under 'Extensions + applications', we can also see 'AzureDiskEncryption', as well:

<img width="2548" height="720" alt="image" src="https://github.com/user-attachments/assets/057901f5-4798-4c58-839f-d028a889d99b" />


