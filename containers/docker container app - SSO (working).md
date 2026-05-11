# Setting Up SSO with Entra ID

While I won't be using it for this personal project, 
I would like to set up SSO to use Entra ID to log in rather than creating a username and password directly through the app itself.

Let's go to the SSO menu and click Create:

<img width="1253" height="484" alt="image" src="https://github.com/user-attachments/assets/8fdb4967-13c7-48e5-9447-e919f33d9fee" />

It'll open this menu, where we will get most of the info from out previously created app registration:

<img width="435" height="1207" alt="image" src="https://github.com/user-attachments/assets/57056d8e-2d36-411d-a586-2f056cd211b3" />

We'll grab our Client ID from here:
<img width="2105" height="360" alt="image" src="https://github.com/user-attachments/assets/172b1317-9022-4e38-b976-b2e95636b636" />

Client Secret from here:
*Create one if not created already. (Note: once you close the client secret menu, the secret will not be visible. Store it somewhere safe or you will need to recreate a new one)*

<img width="1301" height="265" alt="image" src="https://github.com/user-attachments/assets/4a6fb6ab-8ae1-4d03-9f61-acfedff29001" />

Then grab the Endpoint URLs:
We want to use the O'Auth2 URL's

<img width="1044" height="689" alt="image" src="https://github.com/user-attachments/assets/dc4ade05-a5e7-42e0-adbf-e209b07dbc5a" />

For the bottom portion of my SSO setup, I did need help from The Robot (ChatGPT)

<img width="405" height="536" alt="image" src="https://github.com/user-attachments/assets/97841f1d-7d3a-442a-abc5-2d6849a49683" />

The User Endpoint is where Memos calls to get the user information
Scopes is what memos is allowed to be given
And sub, name and email are all attributes to be used for the Entra based Memo profile.

Lets try using our Entra ID:

<img width="532" height="403" alt="image" src="https://github.com/user-attachments/assets/1666518b-cf45-4561-9ba0-d5c0c81e35fa" />

And we're in!

<img width="267" height="559" alt="image" src="https://github.com/user-attachments/assets/3418c81b-5e4c-4bd3-9760-1a7e64d59690" />


