# Setting Up SSO

*This is less specific to the container instance but I will keep it in this thread for organization*

### App Registration

To create and setup SSO with our Entra ID and our container, we will need to setup an App Registration:

We will name the Registration and get the Redirect URL given to us from Memos:

<img width="1226" height="692" alt="image" src="https://github.com/user-attachments/assets/0073c8c6-0f5f-4722-bfe4-5191440b406f" />

We will then create the Registration.

Doing this, we'll get a Client ID and Directory (tenant) ID:

<img width="2196" height="365" alt="image" src="https://github.com/user-attachments/assets/ac461957-b18e-4491-841d-c5efddb03d1d" />


Next, we'll create a Client Secret:
This is how the client will prove it's identity

<img width="1282" height="256" alt="image" src="https://github.com/user-attachments/assets/4e423d31-70a8-46e9-b7d2-645b5af6aa3b" />

Next, we will start filling in our Registered App's Endpoint URLs
(Located in Overview > Endpoint)

<img width="1035" height="1159" alt="image" src="https://github.com/user-attachments/assets/396a697b-2a52-4bea-8900-94386f7ed569" />

We will use the O'Auth 2.0 URLs because that is what Memo uses:

<img width="400" height="1104" alt="image" src="https://github.com/user-attachments/assets/17be3be7-bdb9-4172-a44d-d1f9a0f6912e" />

### Enterprise App Configuration

Registering an app will typically create an Enterprise App as well.
Here you can manage more things not available in the App Registration part of Azure.

We may want to limit what users can access this app through SSO:

<img width="864" height="366" alt="image" src="https://github.com/user-attachments/assets/444f3615-78a8-404b-b1ba-6918b5fc4abd" />

In the Enterprise App section, we get access into setting Conditional Access as well as looking at logs

<img width="256" height="403" alt="image" src="https://github.com/user-attachments/assets/b8f8c204-91af-4f5e-8a79-a9d5bff8266a" />




# Disclaimer with Container Instances

One major disclaimer with Container Instances is that you cannot change things after they are created.
For instance, I want to expose port 443.
Sadly, with Instances, I cannot.

I will retry with Azure Container Apps!
