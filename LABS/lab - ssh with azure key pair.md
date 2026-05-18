# SSH with Azure Key Pair

<img width="150" height="150" alt="image" src="https://github.com/user-attachments/assets/afc700be-603b-44e9-ba6c-38a5c35316d5" />

In this doc, we'll create a Key Pair in Azure (public and private) 
and then configure our Ubuntu Server to use the Key Pair as the only method to remote in.

### Objectives:

We will do the following things:
- Create a Key Pair in Azure
- Create a Ubuntu Server in Azure
- SSH in using the Private Key
- Create another Admin User and use the same Key
- Change the Key pair for the other Admin User for individual Key Pairs

## Create VM and Key Pair Using Azure Cloud Shell



First, we'll create a Resource Group if not created already:
```
cyril [ ~ ]$ az group create --name az104keypair-rg --location EastUs2
```
We get:
```
{
  "id": "/subscriptions/5a8ee2f3-c30e-4ee4-b5ba-446f5ccdb7ae/resourceGroups/az104keypair-rg",
  "location": "eastus2",
  "managedBy": null,
  "name": "az104keypair-rg",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
```
### Create Key Pair

To create a Key Pair, I ran:
```
az sshkey create --name az104keypair --resource-group az104keypair-rg
```
This gives us:

```
No public key is provided. A key pair is being generated for you.
Private key is saved to "/home/cyril/.ssh/1779051366_389425".
Public key is saved to "/home/cyril/.ssh/1779051366_389425.pub".
{
  "id": "/subscriptions/[subscription id]/resourceGroups/AZ104KEYPAIR-RG/providers/Microsoft.Compute/sshPublicKeys/az104keypair",
  "location": "eastus2",
  "name": "az104keypair",
  "publicKey": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDLksCyE9jY0fjPZntNNQ5gbh7+UwUyhIdEahwhFQglB6RuP2/Y2+koCl+OUxqkvL0A68eX11uxIuLlTFGMlT+NRWZQO4pWfejHkYmYDgaffy9zxdoGQ8+ZR2CNgeLjdFZ4veG+RQgewxGI4MHybtkz3VWg1hMd3iZY3UdCs+NMUvA50cRfLLu5kEHYhe4JHo9H2bacOoHB7NnAOAC0ZKcKMvNBAkLaQtyoSm2mFUyoZTjGRiO8/yiOCFoNkNDb7OQx2aDmVYpn5yDfNPaDsLMh80OKyF7KqmkLzbk5p/0tg5MV3efckHDQR2kN8NeY1UeRp7UEV9KUt5ju9iS1fuG28nqgYZKMb/11S/a2Xfvn4MtcabqW6+HEqkBVtsd8NBbyffTVc6ze+AXBuehe0RSCIhkILwQKikQw0P90Gp25LOQ5zGtfcKQBrPj734Nqvxxf2pXZo5+NbiVJQ0d4me3dNYGkUpw6fx+Z1DWGXB52BHV/Wi6/GNl7txK+0selOaE= generated-by-azure",
  "resourceGroup": "AZ104KEYPAIR-RG",
  "tags": null,
  "type": null
}
```

If we go into the Cloud Shell Editor and go into the ``/.ssh`` directory, 
we can find our Public and Private keys.

<img width="491" height="386" alt="image" src="https://github.com/user-attachments/assets/b8773e85-f2e8-470a-ba7b-432f94ee9db0" />

I'll download both keys from the Editor:

<img width="352" height="132" alt="image" src="https://github.com/user-attachments/assets/9d2c2874-1311-49d6-9f01-d51813344b38" />

### Create Ubuntu Server

To create our Ubuntu Server, we'll run:

```
az vm create --resource-group az104keypair-rg --name az104ubuntuserver --image Ubuntu2404 --admin-username cyriladmin --ssh-key-values ~/.ssh/1779048440_9280808.pub --location EastUS2 --size Standard_E2s_v3
```
Our VM is then created:
```
{
  "fqdns": "",
  "id": "/subscriptions/5a8ee2f3-c30e-4ee4-b5ba-446f5ccdb7ae/resourceGroups/az104keypair-rg/providers/Microsoft.Compute/virtualMachines/az104ubuntuserver",
  "location": "eastus2",
  "macAddress": "7C-1E-52-AC-42-80",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "20.7.61.232",
  "resourceGroup": "az104keypair-rg"
}
```
*It may take trial and error to see what SKU and/or VM Size works for you Region. Check with the portal first to see what size limitations you may have*

Let's check our VM and verify that Port 22 (SSH) was enabled by default:

<img width="1815" height="1144" alt="image" src="https://github.com/user-attachments/assets/d6d58ed1-0c65-46b6-b3b7-811b870f4463" />

## Connect with SSH

To connect with SSH, we'll need to first gather a few things:
- The path of our Private Key
- Our VM's Public IP address
- The admin username for the VM

We'll go to our VM and go to **Connect > Connect**

<img width="1062" height="884" alt="image" src="https://github.com/user-attachments/assets/46f6b0c9-3ae3-4134-86e7-cf7dbdb0257a" />

Azure makes it easy for us. 
If we paste in our file path for the private Key, it automatically configures the SSH command we need to run.

Mine will be:
```
ssh -i "C:\Users\cwilliams.DESKTOP-JB54QP9\Downloads\1779048440_9280808" cyriladmin@20.7.61.232
```

Let's try connecting:

I'll open a Command Prompt window and paste my SSH command in.

<img width="1482" height="760" alt="image" src="https://github.com/user-attachments/assets/70db54ad-95b0-431f-ad36-c95b356c8367" />


After entering 'yes', we get this:

<img width="1594" height="1070" alt="image" src="https://github.com/user-attachments/assets/e8508289-e2d4-46c3-b96d-235b0d35a49e" />

## Verify

Let's verify our username, hostname and IP address using:
```
whoami
hostname
ip a
```

<img width="1164" height="472" alt="image" src="https://github.com/user-attachments/assets/ea66c853-06af-4a77-b2ca-7ba0130a4a4d" />


Everything looks correct!

### Stored Public Key

To view our Public Key, if we run:
```
sudo cat ~/.ssh/authorized_keys
```
we can see our Public Key:

<img width="1459" height="172" alt="image" src="https://github.com/user-attachments/assets/537ecae8-0955-4981-976c-3324112c7f1a" />

We can see that it is an RSA key pair, the actual public key data, and that it was generated by Azure!

### Windows Host File

If we go into our Windows Machine and go to ```"C:\Users\cwilliams.DESKTOP-JB54QP9\.ssh\known_hosts"```, 
open with Notepad, we can see server fingerprint:

<img width="1538" height="1003" alt="image" src="https://github.com/user-attachments/assets/e976ac67-ceba-4f13-a740-caa969933bf4" />

*I will be deleting all this later*


### Check for Password Authentication

The way we set up our Server, password authentication should be disabled by default. 

Let's verify that by running: ```sudo cat /etc/ssh/sshd_config```

We'll get:
```
# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no
```

Because the (#) is in front of the line, the Server ignores it. 
This means that Password Authentication is disabled by default!

## Add Another Server Administrator with Same Private Key

Let's say we wanted to add another Admin User to our Server and verify them with the same Key Pair.

Lets do this by creating another User in Ubuntu Server by running:
```
sudo adduser sysadmin
```
<img width="1482" height="760" alt="image" src="https://github.com/user-attachments/assets/5db0cd61-54ee-448d-a4e2-ca2a46fb4e73" />

Let's create them a directory for their SSH key pair and copy it over.

Create Directory: ```sudo mkdir /home/sysadmin/.ssh```

Copy Directory (Keys): ```sudo cp ~/.ssh/authorized_keys /home/sysadmin/.ssh/```

Change Ownership to Other User: ```sudo chown -R sysadmin:sysadmin /home/sysadmin/.ssh```

Verify Keys: 

<img width="1482" height="760" alt="image" src="https://github.com/user-attachments/assets/ff384a25-6517-48fd-80d9-0bf71628ffce" />


We can see we have the same value for both Users.

Let's try logging in with the other Users from Windows:

We'll run: ```C:\Users\cwilliams.DESKTOP-JB54QP9>ssh -i "C:\Users\cwilliams.DESKTOP-JB54QP9\Downloads\1779048440_9280808" sysadmin@20.7.61.232```

<img width="1598" height="848" alt="image" src="https://github.com/user-attachments/assets/6d1152e9-6ddb-4e61-b30d-d5b473a3be4a" />

The Key Pair is recognized and we are granted access!

## Create Second Key Pair for Second Admin User

It's not great practive to use the same Key Pair for more than one user. 
Let's create a 2nd key pair for our SysAdmin user in Azure under 'SSH Keys'

<img width="1068" height="804" alt="image" src="https://github.com/user-attachments/assets/b9899068-1499-4f9a-8e1e-62add6e6ad87" />

We now have our two Azure created Key Pairs:

<img width="2536" height="383" alt="image" src="https://github.com/user-attachments/assets/f7bb585a-3059-42ea-811e-da55ef0fcdcc" />

### Change Public Key

We now want to change the existing key for our Second Admin.

Let's remote back in and change the existing Public Key:

Run this command to change the other Admin's Public Key:
```
sudo nano /home/sysadmin/.ssh/authorized_keys
```

Delete the old Public Key and Paste in the new one from Azure:

<img width="2155" height="606" alt="image" src="https://github.com/user-attachments/assets/3e0498b0-fe6f-4df6-adb4-1eea60e7bcc2" />

Paste the new Public Key in that file path and verify it is the same:

<img width="1776" height="584" alt="image" src="https://github.com/user-attachments/assets/bd459d8e-5e56-48e6-8ff4-89957b2aa860" />

Now try to log in using the newly create Private Key using:
```ssh -i C:\Users\cwilliams.DESKTOP-JB54QP9\Downloads\az104keypair2.pem sysadmin@20.7.61.232```

And we're in:

<img width="1482" height="807" alt="image" src="https://github.com/user-attachments/assets/a4b7e6a1-6cd8-4271-b4d9-8260326d9de0" />

If we try with our original admin account, we get this:

<img width="1018" height="216" alt="image" src="https://github.com/user-attachments/assets/b9368692-f605-45b5-adae-af663fd83d40" />

Bazinga!

