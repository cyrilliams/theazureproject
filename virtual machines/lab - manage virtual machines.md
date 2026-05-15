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

For Networking, we'll let Azure creat our Vnet and Subnet:

<img width="1058" height="756" alt="image" src="https://github.com/user-attachments/assets/20b2c369-d22d-47aa-8fd5-6c3bbc152bca" />

We'll disable 'Boot diagnostics' under 'Managament', then Review and Create.

## Scale Virtual Machine

In the real world, we may need to scale up or Virtual Machine so it has more resources, 
whether RAM or CPU power, it may need to be scaled.

Lets do this now:

Go to our VM, and go to **Availability + scale > Size**

We'll selecet another VM SKU and click Resize:

<img width="2220" height="1092" alt="image" src="https://github.com/user-attachments/assets/ea60bf7c-3158-459b-b6d4-8685dc4b939b" />

This will restart the VM and change the resources the VM has.

### Add Storage Space

To add Storage space via a Storage Disk, we'll go to **Settings > Disks > Create and attatch a new disk**

Choose your configuation and apply!

<img width="2538" height="648" alt="image" src="https://github.com/user-attachments/assets/f9afbbe1-c31d-4eea-88e5-7536086ca16c" />

If we change our mind and want to increase the size or change the type of Disk, 
we can go to the Disk, go to **Settings > Size + performance**, and chose to increase either options.


I'll change to a Standard SSD with 64GBs of Storage:

<img width="2547" height="960" alt="image" src="https://github.com/user-attachments/assets/5d76153b-0b56-4986-a215-b8e4c4fe1433" />

*You will need to stop the VM first to do this*

And now verify the type and size has changed:

<img width="1939" height="444" alt="image" src="https://github.com/user-attachments/assets/0f45119f-cb11-456c-96f4-a55851628310" />

