# Creating an Application Security Group (ASG)

ASG's are a great way to specify the scope of an NSG to multiple virtual machine resources rather than using IP's.
Let's say we want to allow traffic to 5 different VM's, all with different and changing IP's.
Well, in our NSG, we don't want to have to specify the IP,s instead, we want to specify the actual VMs.

Let's quickly create the ASG.

<img width="985" height="378" alt="image" src="https://github.com/user-attachments/assets/c50a7bad-3168-4ae1-a1f5-0be3c783189b" />

Now, you cannot add the VM's into the ASG from the ASG dashboard.
The dashboard just gives you basic information about the ASG:

<img width="2543" height="641" alt="image" src="https://github.com/user-attachments/assets/a4510e89-c202-4971-8ecb-085f4eedaa09" />


In the ASG part of our VM, we will click 'Add'

<img width="2545" height="675" alt="image" src="https://github.com/user-attachments/assets/86bb9ff0-5e8c-450e-b0cb-d2e14d3ebdc6" />

Select our ASG:

<img width="712" height="337" alt="image" src="https://github.com/user-attachments/assets/109cc16b-e7de-4577-9332-7a39bb058348" />

Verify:

<img width="1481" height="580" alt="image" src="https://github.com/user-attachments/assets/6aa574ea-606d-4395-85b8-c5c7997f63a7" />

We can see that the Network Interface and IP are in the ASG and it is attached to the VM and NIC, not just the IP address.

If I changed the IP address, the IP will be updated.

Now, if I create/go to an existing NSG, I can choose my ASG as a destination option:

<img width="715" height="453" alt="image" src="https://github.com/user-attachments/assets/7cc22f44-9252-4796-8d9b-30c023811a90" />

So now, I have all internet web traffic to whatever machines that are in my ASG being blocked inbound:

<img width="2207" height="447" alt="image" src="https://github.com/user-attachments/assets/3cacb228-b52a-40f7-a340-e28ca237ac62" />

