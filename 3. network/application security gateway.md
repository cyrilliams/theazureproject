# Creating an Application Security Gateway (ASG)

ASG's are a great way to specify the scope of an NSG to multiple virtual machine resources rathar than using IP's.
Let's say we want to allow traffic to 5 different VM's, all with different and changing IP's.
Well, in our NSG, we dont want to have to specify the IP,s instead, we want to specify the actual VMs.

Let's quickly create the ASG.

<img width="985" height="378" alt="image" src="https://github.com/user-attachments/assets/c50a7bad-3168-4ae1-a1f5-0be3c783189b" />

Now, you cannot add the VM's into the ASG from the ASG dashboard.
The dashboard just gives you basic information about the ASG:

<img width="2543" height="641" alt="image" src="https://github.com/user-attachments/assets/a4510e89-c202-4971-8ecb-085f4eedaa09" />

*Will come back after VM is re-created*

