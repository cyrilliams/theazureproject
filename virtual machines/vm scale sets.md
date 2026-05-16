*Part of [lab - manage virtual machines](https://github.com/cyrilliams/theazureproject/blob/main/virtual%20machines/lab%20-%20manage%20virtual%20machines.md?plain=1)*

# Deploy Virtual Machine Scale Sets

<img width="279" height="54" alt="image" src="https://github.com/user-attachments/assets/2d1efde3-91c0-4de0-8189-0ef10c1d90fb" />

Let's now create a VM Scale Set, for when we need to scale our VM's automatically when resource needs increase.

Click Create.

We'll start off by Deploying to 3 different Zones, 
as well as choosing Uniform Orchestration mode, for identical VMs.

<img width="1018" height="1092" alt="image" src="https://github.com/user-attachments/assets/2ae05bd1-8113-43cc-bf36-44a8382c21f7" />

We'll choose our Scaling mode and instance count:

<img width="1010" height="986" alt="image" src="https://github.com/user-attachments/assets/02ac84b9-3ae6-447d-a49e-1c029db14009" />

We'll skip the Spot and Disks tab.

Under Networking, we'll create our Vnet and Subnet:

<img width="956" height="579" alt="image" src="https://github.com/user-attachments/assets/c0e0c8e9-c7a6-4cde-819b-ca9593c9d456" />


To create a Network Security Group (NSG) from this part of the Scale Set setup, 
we'll click the Edit or pencil icon on the created NIC for the VM Scale Set:

<img width="1018" height="271" alt="image" src="https://github.com/user-attachments/assets/1f3932e7-dcb0-4864-bb59-945e1308e3d4" />

Click 'Create new'

<img width="990" height="700" alt="image" src="https://github.com/user-attachments/assets/8ec42a1e-f2ce-4462-b223-de07293a7b8e" />


We'll create an inbound rule to allows HTTP traffic:

<img width="2556" height="382" alt="image" src="https://github.com/user-attachments/assets/f21ba438-08cb-4128-8d5c-a210f3b42762" />

Under Load Balancing, we'll use the Azure Load Balancer and quickly create one:

<img width="980" height="452" alt="image" src="https://github.com/user-attachments/assets/e411c171-0e70-40d1-80b7-1ce6596454a8" />

We'll Review + Create.

## Scale Out the VM Scale Set

Now lets configure scaling out or Scale Set

### Scale Out

Now in our VM Scale Set, we'll go to **Availability + scale > Scaling > Custom autoscale**

<img width="1176" height="772" alt="image" src="https://github.com/user-attachments/assets/dc25ed8d-296c-40bc-9709-4861a683b26e" />


We'll create a rule that scales out our Scale Set if the CPU reaches 75% over a 5 minute period:

<img width="723" height="1098" alt="image" src="https://github.com/user-attachments/assets/32703d8e-4bef-4dc2-99f4-333ef1b859ea" />


### Scale In

We may want to scale our Scale Set in when we have less demand. 
Lets configure this:

We'll add a Rule to decrease our VM's by 50% if CPU percentage is less than 20%:

<img width="727" height="1099" alt="image" src="https://github.com/user-attachments/assets/1c1171a6-d603-421f-915c-2b86fa48317b" />

Our Scaling Rules now look like this:

<img width="1152" height="851" alt="image" src="https://github.com/user-attachments/assets/5f728a8b-bed0-465f-a453-4173ed66eabc" />

Great for when demand increases and decreases. 

### Instance Limits

Instance Limits are also great to keep a minimum and maximum amount of VM instances available:

<img width="1091" height="83" alt="image" src="https://github.com/user-attachments/assets/373f0914-a3bc-4be1-b2b2-ed55097ab966" />

Save.

