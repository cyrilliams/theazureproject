# Set Up A Container App

Here, we will re-create our Docker container with Container Apps!

It's very similar to Instances. We will fill out the required info:

<img width="1063" height="1048" alt="image" src="https://github.com/user-attachments/assets/e3763ab7-3f20-4cb3-b3ea-bdc1ba90ac97" />

We'll set the source:

<img width="994" height="701" alt="image" src="https://github.com/user-attachments/assets/dc598abf-876f-4000-846a-46674247a71d" />

Here we'll set the hardware size:

<img width="1064" height="623" alt="image" src="https://github.com/user-attachments/assets/18296a76-be8e-40b5-8773-444cf1254cbf" />

Here we'll set the Ingress (inbound) traffic info:

<img width="986" height="639" alt="image" src="https://github.com/user-attachments/assets/81bcc781-6620-4ba9-b4eb-41a62a9328d8" />

Done!

<img width="2195" height="365" alt="image" src="https://github.com/user-attachments/assets/5a40e6a2-2f2e-4521-80b4-bfc8773a20c5" />

Let's go to the URL:

<img width="2555" height="1064" alt="image" src="https://github.com/user-attachments/assets/d71b9aaf-8ca7-415c-a9c1-17b47c79fa58" />

Nice! Azure Container Apps also automatically configures HTTPS as well!

## Settings Up Our Domain Name 

We will go to our Container App > Custom Domain. 

We'll add our custom domain and verify by adding a TXT and CNAME record:

<img width="704" height="788" alt="image" src="https://github.com/user-attachments/assets/beb6af97-ddbd-417d-a76d-c2603b1aa5d8" />

Let's add that over in our DNS registar:

<img width="1406" height="374" alt="image" src="https://github.com/user-attachments/assets/fe73b918-02c2-48e4-a887-4eaa5ec44c7a" />


Now the domain is added to our Container App.
We'll also add the SNI SSL Certificate

<img width="1402" height="243" alt="image" src="https://github.com/user-attachments/assets/19c5fd65-d23c-4ce6-b183-250f7cc63498" />

Now, lets user our domain name:

<img width="1920" height="1020" alt="image" src="https://github.com/user-attachments/assets/b414ac9b-972f-42d1-89ac-b34cd7b91c73" />

Perfect! It even uses HTTPS!

Now lets setup SSO (again)

Lets setup the Redirect URI with HTTPS

<img width="1545" height="415" alt="image" src="https://github.com/user-attachments/assets/281fe466-dc7b-4b5d-8fa4-4fce833700de" />

Now we'll copy over all the Endpoint URLs




*Will finish*
