# Setting Up DNS For My Container Instance

One major issue with Container Instances (that I found out the hard way) is that when stopped, restarted or interrupted,
the container's public IP is subject to change.
This is an issue if we want to be able to point my domain name to the public IP of the container.

What do we do?

Well, a step that I skipped previously, was to setup a DNS label.
This will create a FQDN (Fully Qualified Domain Name) that will always point to whatever IP the container has at the time.
This is perfect, we get a static domain name for a dynamic IP.
Now, I'll only need to create a CNAME (name to name) record.

Unfortunately, I'll have to rebuild my Container Instance, but that's okay.

Here, we'll add the DNS Name Label 
*(I've covered it for privacy reasons as this part of my lab is a personal project)*

<img width="967" height="576" alt="image" src="https://github.com/user-attachments/assets/e88d6838-566d-4f2d-bd32-23bdd25d9bc6" />


Now, we get a FQDN and Public IP. 

<img width="704" height="217" alt="image" src="https://github.com/user-attachments/assets/068478ac-e6bf-4c33-9bac-749fe0df844f" />

Lets try hitting our container from that FQDN:

<img width="2552" height="991" alt="image" src="https://github.com/user-attachments/assets/f4071c50-687d-491b-b0b5-82693573cb3b" />

**Amazing.**


## DNS Setup

I'll go ahead and add that CNAME record in my DNS registry.
*(I did get a new domain for this as well)*

<img width="1410" height="252" alt="image" src="https://github.com/user-attachments/assets/055944f8-8fbe-4476-951a-db6f49d6b11e" />

In Entra > Domain names, we will register the new domain.

*This part is not technically necessary to setting up with a domain name, but I will implement SSO shortly*

<img width="761" height="621" alt="image" src="https://github.com/user-attachments/assets/ebf5d3dd-00ea-4ea2-8439-b73ad9aea9d4" />

Now, we see that we can use our own domain without having to point to an IP address.

How wonderful!

