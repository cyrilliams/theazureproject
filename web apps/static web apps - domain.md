###### *Consider reading my Static Web App thread first.*

# Migrating My Static Web App URL To My Custom Domain

This part I was very excited about. 
I wanted to be able to hit my website from swa.cyriltest.site rather that 'xxxxx.azurestaticapps.net'

To do this, we will go to 'Custom Domains' in my Static Web App:

**Add** > **Custom Domain**

Now, since we are adding a subdomain, Azure will have us register a CNAME record (which is name to name)

<img width="694" height="605" alt="image" src="https://github.com/user-attachments/assets/82d6bdfc-cd67-4ea7-95ab-970a15b05ecf" />

I'll add this record, pointing to my Static Web App (SWA), and add it as a CNAME record, with the host being '.swa', my subdomain.

<img width="1428" height="497" alt="image" src="https://github.com/user-attachments/assets/9fbfefd5-f56f-4012-bf8f-812e26bbebb0" />

We'll give it a couple minutes to validate and viola!

We can now hit my Static Web App from swa.cyriltest.site:

<img width="679" height="156" alt="image" src="https://github.com/user-attachments/assets/6a573358-8412-4407-8a79-91ea12317cf7" />

Now, we have 2 domains set up.

<img width="2254" height="408" alt="image" src="https://github.com/user-attachments/assets/7783d74a-1e33-4ede-9bbf-3d110edb4812" />



*Note: Azure only allows 2 custom domains, so I believe we would be able to add one more for any reason.*


### Take Away:

This is a great way to host a super simple website with a custom domain for free!
