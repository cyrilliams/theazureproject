# Static Web Apps

Here, we will create a Static Web App, which is a little different from out regular Web Apps.

Static Web Apps are only used to host and run front end code like HTML for a website. .

It has a lot less features than regular Web Apps but is also way more cost effective.

## Creating the Static Web App

I'll apply add it to our applicationsandweb-rg (Resource Group),
name it something relevant,
and select the Free plan

<img width="747" height="713" alt="image" src="https://github.com/user-attachments/assets/8fceedc8-b823-467d-abc9-4c7f49cd0378" />


Next, I'll deploy our code through GitHub:
*I will set up Azure DevOps at a later time to integrate apply CI/CD functions*

<img width="722" height="674" alt="image" src="https://github.com/user-attachments/assets/4423efd8-a938-40cf-94ca-99e404823d8c" />

I'll use GitHub authorization:

<img width="702" height="140" alt="image" src="https://github.com/user-attachments/assets/5a42ca24-286b-4951-95d2-33ae430f7f3d" />

Our free deployment is only available in East US 2, so I'll deploy it there:

*Enterprise Grade Edge would be cool to integrate a CDN but we don't need that.*

<img width="710" height="435" alt="image" src="https://github.com/user-attachments/assets/8a044d2f-7d66-4601-b234-e6ba7624af37" />


Deployed:

<img width="1900" height="561" alt="image" src="https://github.com/user-attachments/assets/8ad82c41-ddf6-4707-92a9-fe1abcb1febb" />



Next, I'll deploy code to the specified repo.

I am using a simple HTML script to deploy a website that just says "Hello World"

*I don't currently know any code besides Python, so I will be learning different languages as I go!*

<img width="1911" height="369" alt="image" src="https://github.com/user-attachments/assets/85317ca4-b5cb-4472-81dd-805532fed75b" />


*After making a small change in the .yml file created in our GitHub repo,* we are now ready to check out our website!

We'll click the URL created by Azure and...

<img width="2274" height="197" alt="image" src="https://github.com/user-attachments/assets/3799a8cb-7313-4d91-9aff-698b05cdff08" />

Viola!

Let's make a change to it from our repo. 
*I made changes through Visual Studio this time*

We'll make the changes, then commit:

<img width="999" height="342" alt="image" src="https://github.com/user-attachments/assets/9f2762a3-4807-44ed-a5c8-4f27b5d5d578" />

Within seconds, Azure has already recieved the changes:

<img width="1450" height="388" alt="image" src="https://github.com/user-attachments/assets/0a7fe243-2d91-4f26-96a0-9ea2fd40ac1e" />

Let's verify:

<img width="1875" height="160" alt="image" src="https://github.com/user-attachments/assets/89ae2bd7-2a97-4e17-bc1a-9303e86f3e79" />




Obviously this is a super simple example, but this is a great way to host front end only code through Azure.


Next, I'll look into changing the URL to my custom domain and using a CI/CD pipeline to push code.

#### Extra:

I went back and changed the title *(what shows on the TAB)* part to "Cyril's Static Web App Test"

<img width="728" height="240" alt="image" src="https://github.com/user-attachments/assets/c1f60fd9-cf68-40ff-8cd2-7f255ff8e413" />

This whole process took less than a minute to commit and deploy.

