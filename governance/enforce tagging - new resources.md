# Enforcing Tags to New Resources

Let's enforce Tags when a Resource is created for better governance over our Resources.

## Enforcing via Policy


We'll start by going to **Policy > Authoring > Definitions**

There are already a ton of built in policies here already:

<img width="1916" height="807" alt="image" src="https://github.com/user-attachments/assets/820a4b87-3b6d-4a0a-8032-6e4494b27167" />

We can filter for the policy we want, which is to 'Require a Tag'

<img width="1640" height="373" alt="image" src="https://github.com/user-attachments/assets/bf8a5f4e-523a-43c7-864c-b66572d66ff6" />

*Notice there are options to require a Tag only or Tag & Values*

Click on the policy.

I'll do 'Require a tag and it's value on resource groups' for this example:

We can see the JSON definition and all other values for the Policy

<img width="1911" height="865" alt="image" src="https://github.com/user-attachments/assets/dd219706-fd3f-4d89-ad1a-4e23d7bb26bb" />

Click 'Assign'

Next, under 'Basics', we'll look at the Policy information and definitions:

<img width="963" height="682" alt="image" src="https://github.com/user-attachments/assets/763ba38d-8178-4527-a3f6-4232deefe34c" />

Under 'Parameters', we'll create a Tag & a Value. We can change these later or create new Tags during Resource creation.

<img width="833" height="332" alt="image" src="https://github.com/user-attachments/assets/4b361302-42f0-4525-8f78-f0dd43b6f7f7" />

We can create a Non-Compliance message if we want:

<img width="1022" height="232" alt="image" src="https://github.com/user-attachments/assets/4ec7e3ce-5eb6-4c56-85be-b456c4e63909" />

Now we have a new Tag enforcement policy:

<img width="455" height="126" alt="image" src="https://github.com/user-attachments/assets/20acb928-4707-4d88-b671-d110ea2e32ea" />



## Verify Tag Enforcement

Let's quickly test our new policy by trying to create a new Resource Group with no Tag:

<img width="799" height="350" alt="image" src="https://github.com/user-attachments/assets/03f50c3d-3ca0-48e8-ada9-1a540b5f3281" />


Under Tags, I'll leave everything blank:

<img width="795" height="281" alt="image" src="https://github.com/user-attachments/assets/398a5854-ff65-4aa1-80a9-fdf647125ab9" />

Now, when I try to go to create the Resource Group, I automatically get a 'Validation failed' error:

<img width="666" height="441" alt="image" src="https://github.com/user-attachments/assets/3aebc123-2de6-49da-8a40-86b6f44b10ab" />

If we go back to the Tag tab, we can see our Policy Non Compliance message:

<img width="921" height="346" alt="image" src="https://github.com/user-attachments/assets/f310fffd-b13a-495d-8e83-c6460d4ad155" />

If we create our Resource Group, we can see it under the assigned Tag:

<img width="1905" height="491" alt="image" src="https://github.com/user-attachments/assets/05ffbc76-576e-40de-b768-2cf4c5347ad9" />

