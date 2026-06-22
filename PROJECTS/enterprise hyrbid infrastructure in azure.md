# Project: Enterprise Hybrid Infrastructure in Azure

In this project, we'll build a small enterprise environment that resembles a real companies architecture.

## Goals

We'll create a hybrid environment that uses a Hub and Spoke topology for networking, Entra ID Connect from my on Prem Windows Server, 
as well as Azure services like Azure Files, Application Gateway, Azure Monitor, Azure Backup & Site Recovery, and RBAC.

## Create Resource Group

First, I'll create a Resource Group to manage and put all of our resources into:

<img width="821" height="425" alt="image" src="https://github.com/user-attachments/assets/42194000-8365-4520-8707-dc495d69fe01" />


## Create Networks

<img width="92" height="97" alt="image" src="https://github.com/user-attachments/assets/052067c2-b2c3-4c36-bf0f-d657e1fe57b4" />

*I changed the RG to the correct RG after*

After, let's creat our Hub and Spoke V-Nets.

### Hub V-Net

We'll start with the Hub, which will represent the main branch/core location.

<img width="801" height="691" alt="image" src="https://github.com/user-attachments/assets/ccf73368-1f92-4190-be94-63dc6d40f4e9" />

We'll use the 10.0.0.0/16 address space.

We'll then create 3 subnets: GatewaySubnet, Management and SharedServices. Each will use the 10.0.0.0/24 address space.

<img width="824" height="728" alt="image" src="https://github.com/user-attachments/assets/767c419a-f404-4757-90c5-ccdd406bc696" />

We'll create and move to a Spoke V-Net

### Spoke V-Net

Next, we'll create our next V-Net. This will be modeled after a sub-location:

<img width="838" height="612" alt="image" src="https://github.com/user-attachments/assets/44197630-b346-47e3-8349-0df85168df34" />

We'll give it a 10.1.0.0/16 address space and two Subnets: Web and Application:

<img width="735" height="599" alt="image" src="https://github.com/user-attachments/assets/21dd110b-3b79-44c0-9d5a-06530168c486" />

### Implement Connectivity with V-Net Peering

We want these two V-Nets to talk to each other. Let's enable peering between the two.

Let's go to our Main Location V-Net, **Settings > Peerings > Add**

<img width="844" height="766" alt="image" src="https://github.com/user-attachments/assets/9d77c485-be43-4e8e-9fd0-a2709f863eb8" />

Now, if we go into our Lake Worth V-Net, we can see Peering has been enabled as well:

<img width="1330" height="679" alt="image" src="https://github.com/user-attachments/assets/1c9ddce8-75ea-466d-9ff8-d91040ab3128" />


## Connect On Premises Windows Server and Connect Identity

For this part, we'll connect our on Prem Windows Server running Active Directory to our Azure tenant.

Here we have created an OU called Lake Worth, but have no members in it. Let's add a member named "Billy Bob", who is a Manager.

<img width="1440" height="900" alt="image" src="https://github.com/user-attachments/assets/658c5c74-8f2e-4e74-b448-d915dbc00c3d" />

Next, let's donwload the Azure Connect agent from Entra ID, under **Entra ID > Entra Connect**

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/701e4aec-9a6f-44fd-8e51-be3048798ee4" />

We'll sign in and go through the prompts:

<img width="920" height="652" alt="image" src="https://github.com/user-attachments/assets/b5b99553-694b-4c1f-a291-875e8de4976d" />

Enter our on Prem admin credentials:

<img width="911" height="652" alt="image" src="https://github.com/user-attachments/assets/1f1e03b7-814a-45f9-9bfb-4c457f0ed5bd" />

Install:

<img width="937" height="664" alt="image" src="https://github.com/user-attachments/assets/56eac812-d0e8-4b28-a3ed-eefacb874a1b" />


