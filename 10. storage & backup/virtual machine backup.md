# Create a Virtual Machine Backup

In this doc, we'll create a back up of a Virtual Machine using a Recovery Services Vault.

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
