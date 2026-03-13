# Creating a Custom RBAC Role

Let's say we wanted to make a custom role that allowed a user to only Start, Power Off and Restart Virtual Machines.

Let's go to our Subscription > Add > Add custom role

![alt text](image.png)

We'll give it a name and description:

![alt text](image-1.png)

Next, we'll add permissions. Here's where it get's granular:

Let's select 'Microsoft Compute'

![alt text](image-2.png)

We'll scroll all the way down to 'Microsoft.Compute/virtualMachines' and select the controls we want this role to have.

We can see we can choose what actions the user is allowed to read or write. It can get very granular, which can be good!

![alt text](image-3.png)

We can verify our permissions for this role:

![alt text](image-4.png)

We can also select this Scope of this role. 

So if we only want our user to be able to start and stop VM's that are in a certain Resource Group, we can do that here:

![alt text](image-5.png)

I'll just let this user start and stop any Virtual Machine is our Subcription.

Let's observe and review the JSON:

We can see all ther permissions that we gave this role:

![alt text](image-6.png)

