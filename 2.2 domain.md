# Setting Up My Domain

In this lab, I will be buying and configuring my domain, as well as getting it linked to Azure.

I used namecheap.com to buy a super cheap test domain: **CyrilTest.Site**

## Setting up DNS

Currently, I'll use NameCheap's BasicDNS Name Servers which are:

    dns1.registrar-servers.com
    dns2.registrar-servers.com

This is essentially me stating that I want the authoritative source and go-to for my domain will be NameCheap's DNS servers.

<img width="1151" height="761" alt="image" src="https://github.com/user-attachments/assets/a50eeef6-be15-45df-b066-c2382b98e784" />


## Setup Custom Domain

I'll setup a custom domain next. Entra gives me a destination to give to my registrar as a TXT record:

<img width="571" height="248" alt="image" src="https://github.com/user-attachments/assets/bd4964e0-5788-471f-9f4d-f2d56a88bd51" />

I'll go ahead and enter that in as a TXT record in Namecheap:
(I've blocked the record info just in case)

<img width="1112" height="54" alt="image" src="https://github.com/user-attachments/assets/f5da0f30-4d29-4cb5-ac3b-57fed65f875b" />

I believe now, I'll have to wait a bit. I will come back to this in 30 minutes to an hour!

After about an hour, we have successfully verified our domain!

<img width="352" height="89" alt="image" src="https://github.com/user-attachments/assets/a6e7bdd3-8b42-4195-9b59-773f84964e36" />

Now we will make that the primary domain:

<img width="391" height="112" alt="image" src="https://github.com/user-attachments/assets/a61859d6-3944-4956-aecb-a6fbba3ef912" />

I'll also change my users to have the same domain:

<img width="893" height="606" alt="image" src="https://github.com/user-attachments/assets/8246feec-1e75-46cd-a52a-de86da7c3e78" />




# Extra Steps But Not Necessary

Here I set up Verified ID and Azure Key Vault. I thought I needed both of these to register and manage my organization.


## Setup Organization

We will also get started in registering our domain in Entra, as well as setting up our organization.

<img width="1316" height="869" alt="image" src="https://github.com/user-attachments/assets/5003bbe7-1e76-463c-9993-596c04eec57c" />


Here we will input the organization name as well as the domain itself. 
**Custom domain must be set up, as stated in the Microsoft Documentation)

<img width="692" height="282" alt="image" src="https://github.com/user-attachments/assets/f7724371-2106-46f3-ad9c-4f1a6057b400" />

## Azure Key Vault

Next, we will setup Azure Key Vault.
This is because we need to store a secret, (an SSL certificate in this case), that may be needed to link our domain to apps and services that we will be using.

<img width="764" height="633" alt="image" src="https://github.com/user-attachments/assets/d4725d7a-5967-459d-9f90-f4a81fd6d72d" />

For the networking portion, I'll enable public access and allow only my created networks to access the Key Vault.
*This will be easier for now than setting up private endpoints and is still very secure!*

<img width="759" height="662" alt="image" src="https://github.com/user-attachments/assets/c0ecd00b-1f3a-4e7c-84bb-5f5e72e0ce3a" />




