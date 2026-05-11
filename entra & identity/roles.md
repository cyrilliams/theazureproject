# Understanding Roles

One thing I was failing to understand was the difference between roles in Azure and Entra.
Earlier, I was getting stuck while trying to let my Admin account create a Key Vault.
I had assigned it the Global Admin role in Entra, so why couldn't I do what I needed to?

Well, this was because I was not understanind RBAC (Role Based Access) and Entra roles

### RBAC (Role Based Access)

This defines more what you can do and touch things in Azure such as creating Resources, Resource Groups, etc at a Subscription level.

### Entra Roles

This defines more of what a user can do at a tenant wide level (which is more tied to Identity and the company/organization)
