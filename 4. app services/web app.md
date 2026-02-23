# Creating a Web App

### What is a Web App?

A web app is a PAAS (Platform as a Service) that allows you to create and run applications without managing the actual infrastructre such as servers and networking resources.

This is useful for something as simple as a website, 
where maybe we don't want to deploy our own server, or deploy a dedicated Virtual Machine,
but only want to create the necessary resources to create and host the website.

You can option to use code or create a container.

I'm going to option to create the deployment and run with code:

<img width="708" height="472" alt="image" src="https://github.com/user-attachments/assets/859cf940-8ec8-4b1e-a17e-e69b07b96abf" />

For cost purposes, I'm going to use the free pricing plan which uses shared infrastructure:
*No redundancy is included here, which is fine*

<img width="720" height="422" alt="image" src="https://github.com/user-attachments/assets/b1a16c9a-2d6f-4df0-a0d9-86fa1f842ae6" />

I'll skip all the unnecessary options that are not needed and create my Web App:

<img width="689" height="684" alt="image" src="https://github.com/user-attachments/assets/0131f553-d78a-4941-97c8-7b132a9f7434" />

The deployed app has now been created:

<img width="1635" height="797" alt="image" src="https://github.com/user-attachments/assets/0cda9029-3bd4-4e3d-a705-79fc8a407d69" />

#### Things To Note (Free Tier):

I was trying to deploy the Web App in East US, but kept getting an error.
I validated the rest of my settings and tried again with East US 2 and Southcentral US, still getting the same error.

After looking into this more, I found that the free tier for webapps may not be supported in some regions due to capacity restraints. 

I redeployed in Canada Central and my Web App deployed with no issues.
