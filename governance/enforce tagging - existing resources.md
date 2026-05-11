# Enforce Tags for Existing Resources

In this doc, we'll enforce Tags for Resources that do no have Tags already:

## Enforcing via Policy

We'll start by going to **Policy > Authoring > Assignments > Assign policy**

Name the tag. For this Policy, we'll call it 'Inheret tag'

<img width="898" height="637" alt="image" src="https://github.com/user-attachments/assets/beb88d2d-468c-4c56-9f82-9c52aaea60b8" />

Under 'Policy Definition', find and select the 'Inheret a tag from the resource group'

<img width="839" height="378" alt="image" src="https://github.com/user-attachments/assets/d59159a5-1186-4562-ab38-2327f9287991" />

Verify it on the Basics tab:

<img width="741" height="123" alt="image" src="https://github.com/user-attachments/assets/c07aa4cc-7bf7-426d-b26a-92381a8b980e" />

Under 'Parameters', we'll assign a Tag:

<img width="874" height="192" alt="image" src="https://github.com/user-attachments/assets/e29f2c7a-5d93-48dc-b3b9-fc23f856702b" />

Under 'Remediation', enable 'Create a remediation task and leave the default 'Policy to remediate'

<img width="829" height="351" alt="image" src="https://github.com/user-attachments/assets/ebe42f47-992a-4abb-8431-6a5ec9bd2271" />

We'll create the policy and verify it!

<img width="347" height="278" alt="image" src="https://github.com/user-attachments/assets/4cf5f5d4-ce63-4b86-a959-4e932b470629" />

## Verify

Next, I'll create a Resource. I'll create a Storage Account as an example.

<img width="933" height="869" alt="image" src="https://github.com/user-attachments/assets/0879c966-7d94-4673-8c6c-91f8d7582c99" />

We can see that it has no Tag assigned:

<img width="1051" height="319" alt="image" src="https://github.com/user-attachments/assets/b14da3bc-6fbc-477c-8f65-e6cd1cc455f4" />

After creating the Storage Account, under Tags, we can see the Tag (Location : Florida) was automatically applied!

<img width="1910" height="688" alt="image" src="https://github.com/user-attachments/assets/950e71b2-2828-4fbf-ad6f-af847e8ce0d1" />

## Verify - Assign Policy to Resource Group

A step I initially missed was making sure the policy I assigned was to the Resource Group itself.

Under the selected Resource Group, go to **Settings > Policies**

<img width="1331" height="691" alt="image" src="https://github.com/user-attachments/assets/66efc968-4e96-4eb2-a697-72e3d1124fd1" />


Verify or create your Policies here to apply them to a specific Resource Group!

<img width="1325" height="654" alt="image" src="https://github.com/user-attachments/assets/126ca7a5-5e38-4631-b727-71299e6cb81d" />

### Policy with No Tag

I have another RG with the policy assigned but no Tag.

<img width="1327" height="657" alt="image" src="https://github.com/user-attachments/assets/1e332f07-04cd-4ba8-b827-a4919a44aada" />

I have an Key Vault with no Tag in here as well:

<img width="1905" height="524" alt="image" src="https://github.com/user-attachments/assets/34ffe975-06b8-4f11-a359-629c73d63b23" />

If I go back and create a Tag for the Resource Group, it will automatically apply to my Resource:

<img width="1329" height="455" alt="image" src="https://github.com/user-attachments/assets/6306aac0-5e48-4852-a7bf-de6db9d06c47" />

Let's check the Key Vault:

<img width="1906" height="450" alt="image" src="https://github.com/user-attachments/assets/246eaf08-c809-411d-af02-d7ce6d86e467" />

We can see that it has now automatically applied the Tags to the Resource within the RG.

This can be good if you have a lot of reources that need to be Tagged.
