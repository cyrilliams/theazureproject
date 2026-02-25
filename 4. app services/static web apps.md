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



*My github currently does not have any code in it. We will deploy that soon*



Stopping point: next we will deploy the code and setup up the SWA with our custom domain
