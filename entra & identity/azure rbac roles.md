# Add an Azure RBAC Role

We just created a user and have him a Reader role in Entra, let's give that user Roles on the Azure side of things.

We'll first go to our Subscription > Access control (IAM) > Add > Add role assignment

<img width="1039" height="332" alt="image" src="https://github.com/user-attachments/assets/988e4216-affd-4344-86e4-3cd45c797ccf" />

We'll select the Reader role:

<img width="1905" height="532" alt="image" src="https://github.com/user-attachments/assets/a3cd03e0-6e43-4efa-9ce7-00f6bfbd0b4b" />

You can select a specific user, or add a group, to give the roles to.

<img width="1215" height="487" alt="image" src="https://github.com/user-attachments/assets/be7341ad-34b9-4165-a3d1-4b9b0f74a0b8" />

Now we'll click 'Review + assign' and add that role:

<img width="447" height="87" alt="image" src="https://github.com/user-attachments/assets/8983c519-cc35-4549-9fad-92520a89184b" />

Now being logged into my Reader account, I can actually see Azure Resources:

<img width="1917" height="326" alt="image" src="https://github.com/user-attachments/assets/ebdf74c8-6ad8-4e42-93e9-7b3dad5858b7" />

### Verify

Let's make sure though, that I cannot create or manage Resources:

In my Reader account, let's try to create a Subnet:

We can see here that it immediately errors out:

<img width="337" height="271" alt="image" src="https://github.com/user-attachments/assets/1f49eb94-17cb-4f8c-a960-4670fab00aa9" />

We can also try editing the available Subnets but the options are greyed out:

<img width="839" height="863" alt="image" src="https://github.com/user-attachments/assets/bdddba4d-7d88-41cd-971a-54fe49b4d14a" />

Nice!

---

It's important to understand Roles in Azure and Entra. That was a concept I was mixing up.
