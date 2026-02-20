# The Gateway

Now that we have the VM going, we need to setup a VPN gateway to:
1. Be able to remote onto my existing VM
2. Setup subnet peering and site to site connections so all of my devices can talk to each other!

Here, we'll create the VPN gateway:

<img width="942" height="988" alt="image" src="https://github.com/user-attachments/assets/fa31cf28-9bb2-43fb-b61a-edefc14427a2" />

We'll create a public IP since we will need at least one to route and connect to it over the internet:
*We will skip and disable all the unnecessary stuff like configuring BGP and active mode*

<img width="948" height="514" alt="image" src="https://github.com/user-attachments/assets/7f7b7b24-1fdd-415b-95e9-cc00331b5124" />

## Errors

I did get this error when trying to create the Gateway

<img width="673" height="227" alt="image" src="https://github.com/user-attachments/assets/44b0f172-4522-469c-932a-d66ba32818d3" />

After a bit of research, I had totally forgotten that the Gateway requires it's own subnet.
We'll create that here:

<img width="1039" height="557" alt="image" src="https://github.com/user-attachments/assets/9cca13e3-4d68-4997-b7f8-a931e543dac8" />


Now if we go back to create the Gateway, the GatewaySubnet automatically comes up!

<img width="940" height="174" alt="image" src="https://github.com/user-attachments/assets/61bd7475-c592-4919-969f-31356097f387" />

Gateway now created and deployed!

<img width="1509" height="124" alt="image" src="https://github.com/user-attachments/assets/96f6f59f-b974-4cfb-b21e-86cc9b06dba9" />




