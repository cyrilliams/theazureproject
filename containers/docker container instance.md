# Creating a Container Instance with Docker Hub

In this section, we will create and deploy a Docker container via a Container Instance.

The reason we are doing a Container Instance and not a Container App or running a Virtual  Machine running a server image on it is because I would like to deploy just one image with no need to scale up or down or in or out.

For scaling containers, Container Apps or a Kubernetes service would be best.

### Setup

Here, I'll assign the right Resource Group, add an appropriate name and select the region.

<img width="834" height="758" alt="image" src="https://github.com/user-attachments/assets/01fa3519-7042-4c05-bffe-cd3f2b45d4e1" />

We will check 'Other Registry', which will default to Docker Hub.

Luckily the container I want, Memos, is on Docker Hub

<img width="1910" height="557" alt="image" src="https://github.com/user-attachments/assets/a8010dd1-67e6-4cea-8314-93fdb05e7e86" />


We will specify the image source: 

The URL is: *https://hub.docker.com/r/neosmemo/memos*

But we will specify 
ghcr.io/usememos/memos:latest
*The ':latest' will pull the latest version of the container*


Last thing here is to select the hardware size. I'll choose a very low specification:

<img width="570" height="395" alt="image" src="https://github.com/user-attachments/assets/9c9c380a-507a-4913-b394-d24b3f874ea5" />

### Networking

We will enable a Public IP for the container, since I would like the container to be hit from anywhere.
We also will specify the Port # which is 5230 over TCP, which is the port Memos uses:

<img width="779" height="439" alt="image" src="https://github.com/user-attachments/assets/f60a43c9-8787-4987-a717-507a748e9b09" />


We'll skip to the end and validate:
<img width="1900" height="735" alt="image" src="https://github.com/user-attachments/assets/a62ab17f-d6af-4355-8492-f7a95ee9db5c" />

### Deployment Errors:

Our container instance failed. After a little time with The Robot (ChatGPT), I had the repository set incorrectly.
I was trying to pull the repo from the Docker Hub URL. 
The Robot gave me the correct location which was ghcr.io/usememos/memos:latest

<img width="753" height="648" alt="image" src="https://github.com/user-attachments/assets/bdcba6be-1109-458b-8af6-93fc20882103" />

Our deployment was a success!

<img width="1902" height="752" alt="image" src="https://github.com/user-attachments/assets/f41f389e-f745-4034-a88e-912c63822e61" />


Now, if we hit our Public IP that was given to us and specify the port 5230, we should see:

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/4cce8659-2f4b-4f65-bf43-7424969da540" />


# Rebuild Docker Container to work with DNS

While we are able to reach our container over the Public IP and port number,
We want to be able to set up our domain and point that IP and port to a domain name.

Unfortunately, Container Instances do not support port forwarding or any type of forwarding.
So, we will rebuild the container and use Port 80 be used when we setup or DNS record.

We'll do that by changing the environment variables here:
*Instead of using 5320, we will change it to 80*
<img width="949" height="424" alt="image" src="https://github.com/user-attachments/assets/ff6bc9f4-4538-4975-a881-dd213d33199f" />

As well as allow Port 80:
<img width="795" height="446" alt="image" src="https://github.com/user-attachments/assets/49a201fd-5936-4fb7-84f8-0b0bbe78c53c" />

Now, I can hit Memos with just the IP without specifying the port (because all traffic over the internet is automatically 443 or 80)

<img width="1913" height="984" alt="image" src="https://github.com/user-attachments/assets/006c7122-3fb7-4cae-af53-c203157a8932" />



