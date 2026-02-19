# Setting Up My Domain

In this lab, I will be buying and configuring my domain, as well as getting it linked to Azure.

I used namecheap.com to buy a super cheap test domain: CyrilTest.Site

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


## Setup Organization

We will also get started in reistering our domain in Entra, as well as setting up our orgainzation.

<img width="1624" height="651" alt="image" src="https://github.com/user-attachments/assets/fc3623ec-d8d4-4099-a363-0d8d5e6279e6" />

Here we will input the organization name as well as the domain itself.

<img width="692" height="282" alt="image" src="https://github.com/user-attachments/assets/f7724371-2106-46f3-ad9c-4f1a6057b400" />

## Azure Key Vault

Next, we will setup Azure Key Vault.
This is because we need to store a secret, (an SSL certificate in this case), that may be needed to link our domain to apps and services that we will be using.

<img width="764" height="633" alt="image" src="https://github.com/user-attachments/assets/d4725d7a-5967-459d-9f90-f4a81fd6d72d" />

For the networking portion, I'll enable public access and allow only my created networks to access the Key Vault.
*This will be easier for now than setting up private endpoints and is still very secure!*

<img width="759" height="662" alt="image" src="https://github.com/user-attachments/assets/c0ecd00b-1f3a-4e7c-84bb-5f5e72e0ce3a" />




