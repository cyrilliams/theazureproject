# Deploying a Virtual Machine with Powershell

Azure lets us create VM's using Powershell! 
Whether its Powershell native to your PC, or Azure's Cloud Shell, we will be able to create and configure a VM through command line.

First, we will make sure we switch from Bash to Powershell

<img width="1016" height="218" alt="image" src="https://github.com/user-attachments/assets/a8f1b636-953c-4cf9-ba6a-be365714ffe2" />


### Create Resource Group

Although I already have one, 
let's create a new recourse group through PS as well with the commands:
```ps1
New-AzResourceGroup -Name 'myResourceGroup' -Location 'centralus'
```

Now, we have our first Powershell based resource group:

<img width="1190" height="207" alt="image" src="https://github.com/user-attachments/assets/15051c63-f470-477b-872a-50c0a4b149f7" />

### Create the Virtual Machine

Next, we will use this template from Microsoft Learn to customize and set parameters for this Virtual Machine:
```ps1
New-AzVm -ResourceGroupName 'myResourceGroup' -Name 'myVM' -Location 'centralus' -Image 'MicrosoftWindowsServer:WindowsServer:2022-datacenter-azure-edition:latest' -VirtualNetworkName 'myVnet' -SubnetName 'mySubnet' -SecurityGroupName 'myNetworkSecurityGroup' -PublicIpAddressName 'myPublicIpAddress' -OpenPorts 80,3389
```

I'll change the Resource Group, name and location. 
It'll then ask me to create an admin user and password:

<img width="1818" height="345" alt="image" src="https://github.com/user-attachments/assets/e107a053-9172-4eab-89b4-e3511b203fe8" />

*Take note that because we did not specify the SKU for the VM, it used the Standard_D2s_v3 SKU*

*I believe that all we technically need to create a VM is the resource group, name and location, and Azure will auto default the rest*


Our VM has now been created via Powershell:

<img width="1845" height="420" alt="image" src="https://github.com/user-attachments/assets/598c36a6-37ea-4b16-ba7b-ec93c8b904cb" />

Now if we go to our list of VM's, we can see it's created:

<img width="2198" height="303" alt="image" src="https://github.com/user-attachments/assets/25c2b64f-ccf8-479e-916d-db6ef4179236" />

Pretty cool stuff!

---

### Removing the Resource Group and VM

I want to keep my money so I will stop the VM and then remove the VM and everything I just created in that resource group with this command:
```ps1
Remove-AzResourceGroup -Name 'myResourceGroup'
```
<img width="696" height="163" alt="image" src="https://github.com/user-attachments/assets/883debb9-522e-432d-a8e1-e94c0eec540e" />

After a bit of waiting, no more VM:

<img width="2212" height="848" alt="image" src="https://github.com/user-attachments/assets/dbff00db-de47-42c5-85ce-617c3ead9d65" />

Nice. My wallet will thank me later.


