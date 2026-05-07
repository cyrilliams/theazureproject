# Create a Resource Lock

In this doc, we'll create a Resource Lock. This prevents accidental deletion of Resources:

# Delete Type Lock

Under the Resource Group, we'll go to **Settings > Locks > Add**

<img width="691" height="684" alt="image" src="https://github.com/user-attachments/assets/45a751e1-bf10-4444-bfb5-2359862db25a" />

We'll name it and change the 'Lock type' to 'Delete'.

<img width="1644" height="186" alt="image" src="https://github.com/user-attachments/assets/e7a57e3e-f9a3-47e2-b9d0-a60e364d1bd0" />

## Verify

Let's try deleting the RG, which is the scope of the Lock

<img width="462" height="184" alt="image" src="https://github.com/user-attachments/assets/32154014-e7d2-43c2-88d7-52e6b9808cd7" />

When we click Delete, we are met with an error:

<img width="462" height="184" alt="image" src="https://github.com/user-attachments/assets/588bd8b0-2bfb-434d-ab1b-7e34b61ba1b1" />


# Lock Types:


## Delete Lock (CanNotDelete)
Purpose: Prevents deletion only.
What it does

✅ Allows read operations
✅ Allows update / modify operations
❌ Blocks delete operations on the resource

Example

You can:

Resize a VM
Update tags
Change configuration


You cannot:

Delete the VM
Delete a resource group containing that VM



Typical use cases

Production resources where:

Changes are expected
Deletion must be prevented (accidental or unauthorized)



✅ Most commonly used lock
---
## Read-only Lock (ReadOnly)
Purpose: Prevents any changes.
What it does

✅ Allows read operations
❌ Blocks update
❌ Blocks delete

This effectively makes the resource immutable.
Example

You can:

View configuration
Read metrics


You cannot:

Change size or settings
Start/stop a VM
Modify tags
Delete the resource




Azure treats almost all write operations as changes — even starting/stopping a VM is blocked.

Typical use cases

Compliance or audit scenarios
Reference resources (gold images, baseline configs)
Temporary freeze during investigations or incidents

⚠️ Used sparingly because it blocks normal operations

# Delete Resource/RG

To delete the Resource or RG, delete the Resource Lock.
