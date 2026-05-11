# Creating a Custom RBAC Role

Let's say we wanted to make a custom role that allowed a user to only Start, Power Off and Restart Virtual Machines.

Let's go to our Subscription > Add > Add custom role

<img width="679" height="289" alt="image" src="https://github.com/user-attachments/assets/75cf9df6-c4ec-4d53-a0af-7de2e7efefa9" />

We'll give it a name and description:

<img width="1067" height="370" alt="image" src="https://github.com/user-attachments/assets/b28ffca2-5720-4abe-ae29-873674311eda" />

Next, we'll add permissions. Here's where it get's granular:

Let's select 'Microsoft Compute'

<img width="1082" height="800" alt="image" src="https://github.com/user-attachments/assets/8b2d179d-e3a7-41ad-aef8-825d4c4c2e70" />

We'll scroll all the way down to 'Microsoft.Compute/virtualMachines' and select the controls we want this role to have.

We can see we can choose what actions the user is allowed to read or write. It can get very granular, which can be good!

<img width="1102" height="851" alt="image" src="https://github.com/user-attachments/assets/0437bcb2-6830-4812-b0f3-4d02c7f21aa9" />

We can verify our permissions for this role:

<img width="1368" height="317" alt="image" src="https://github.com/user-attachments/assets/5ed9a35f-19dc-4a07-9912-ca3a7126ff31" />


We can also select this Scope of this role. 

So if we only want our user to be able to start and stop VM's that are in a certain Resource Group, we can do that here:

<img width="1102" height="776" alt="image" src="https://github.com/user-attachments/assets/e4a0b47f-1f29-47b7-ab2d-497c7113fbd2" />


I'll just let this user start and stop any Virtual Machine is our Subcription.

Let's observe and review the JSON:

We can see all ther permissions that we gave this role:

<img width="1348" height="605" alt="image" src="https://github.com/user-attachments/assets/2167a270-f794-48a9-b978-b492eebcb3df" />


After, we'll  click 'Review and create'

### Assign Role to User

We can see our new Role in the Roles section of Access Control (IAM)

<img width="1907" height="774" alt="image" src="https://github.com/user-attachments/assets/1facb40f-b54d-4b3a-8264-cfeb1114a830" />


Let's click 'Add' and select our new Custom Role and add a Member:

<img width="1213" height="506" alt="image" src="https://github.com/user-attachments/assets/467bb081-02da-4e35-af45-ae9c6eb9a084" />


Now if we look in our Role Assignments, we can see it's been added to our Reader user:

<img width="1635" height="555" alt="image" src="https://github.com/user-attachments/assets/77ce3617-821f-4677-a068-d4fa82a8fda2" />


### Verify

Just to check these Role Permissions are in affect and working, I'll create a VM quickly.

Let's sign in to our Reader account and try to verify and test out our new permissions:

<img width="847" height="408" alt="image" src="https://github.com/user-attachments/assets/900f8242-71ca-422b-8765-85a31b0731df" />


Let's try to start our VM:

<img width="1910" height="461" alt="image" src="https://github.com/user-attachments/assets/95605279-4fdf-4a76-b8c9-1c5447604b8b" />


It was successful!

<img width="470" height="290" alt="image" src="https://github.com/user-attachments/assets/4579a699-da78-49b9-a0c5-a3843e6ea6a6" />


*I tried stopping the VM from the Reader account and was not successful. After further research, we also need to add the deallocate permission in the role as well. I'll add that to the role quickly*

<img width="1360" height="318" alt="image" src="https://github.com/user-attachments/assets/ff035ce7-19fa-4025-976b-88c7a5e8c2d0" />


After signing in and out of my Reader account, I was able to stop the VM:

<img width="470" height="260" alt="image" src="https://github.com/user-attachments/assets/1df5646c-3a4a-4c41-a846-e90c87777e71" />


When trying to delete the VM, I am met with this error:

<img width="443" height="341" alt="image" src="https://github.com/user-attachments/assets/d77ac347-b670-46ee-8019-6ed8fb2d6168" />

Very nice!
