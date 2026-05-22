# App Service Plan

<img width="107" height="105" alt="image" src="https://github.com/user-attachments/assets/634ae800-9255-419b-ad70-c9e89b1c72e6" />

In this doc, we'll go over Azure Web Service Plans and how they function as a PaaS (Platform as a Service)

## Create App Service Plan

We'll start by creating the App Service Plan:

<img width="837" height="742" alt="image" src="https://github.com/user-attachments/assets/16bdf894-71cc-48df-bdb4-cda6e491c996" />

*Notice that we have the option for the Operating System.
ASP's run either Linux or Windows. We do not have to manage the OS at all, only the Apps themselves.
We can think of the ASP as a Hypervisor or Cluster
This is what makes ASP's a great PaaS option*

### Plans

ASP's have multiple plans that we can use:

<img width="437" height="411" alt="image" src="https://github.com/user-attachments/assets/6cd9d8e7-5136-46c7-9307-ba9297572890" />

*We can see the difference in CPU and Memory, as well as Cost, from the higher Premium options.*

I'll choose the Basic B1 option.

### Zone Redudancy

We can also see that Zone Redudancy is not available for the Basic plan. It is available for the Premium plans, though.

<img width="734" height="488" alt="image" src="https://github.com/user-attachments/assets/04e09126-fc12-480e-8443-b9d00eff1762" />

We'll Review + Create

## Create App Services (Web Apps)

### Web App 1

Now, we will create our App Services (Web Apps). 
These will sit in our App Service Plan and run on that infrastructure.

We'll go to **App services > Create > Web App**

<img width="767" height="809" alt="image" src="https://github.com/user-attachments/assets/ecb258fa-7767-4243-91c7-181fee415553" />

Select the App Service Plan at the bottom.

#### Runtime Stack & Operating System Limitations

It is important to note that the Windows plan cannot run Python as a Runtime Stack, as well as the Linux plan is not able to run .NET.

All other available Runtime Stacks are avaiable for both plans.

### Web App 2

I'll create the 2nd Web App from a Template of the first Web App.

In the Parameters, the only change I'll make is the name of the Web App and the Runtime Stack:

**Name:**
```json
"name": {
      "value": "cyrilaz104-webapp2"
    }
```
**Linux Runtime Stack:**
```json
"linuxFxVersion": {
      "value": "PHP:8.5"
    }
```

It should look like this:

<img width="858" height="795" alt="image" src="https://github.com/user-attachments/assets/e6055293-4b3f-40b0-b746-f4456b42cb9f" />

We'll review our 2nd Web App and create it:

<img width="1018" height="775" alt="image" src="https://github.com/user-attachments/assets/64a1c4d2-5f6c-4484-adc0-88d9fcbcb77a" />

### Verify

Now, if we check our Resource Group, we have both of our Web Apps:

<img width="1904" height="518" alt="image" src="https://github.com/user-attachments/assets/9246373f-7d05-4c1b-a38a-08925921bf8f" />

If we check within our App Service Plan and go to **Settings > Apps**, we have our 2 Web Apps under our Service Plan.

<img width="1910" height="446" alt="image" src="https://github.com/user-attachments/assets/f0341b36-35fa-44ff-a83f-e000bdebbb8e" />

## Scale Up (More Resources)

In our App Service Plan overview, we can see that the Memory is at 70%+ usage.
Let's scale up our ASP and add more resources:

Under our ASP, we'll go to **Settings > Scale up (App Service plan)**

Let's scale up from the Basic B1 to the Premium v3 P0V3 SKU.

<img width="1906" height="819" alt="image" src="https://github.com/user-attachments/assets/3397432d-a45f-4286-b437-a62e53974d51" />

Back in the Overview tab, we can see our plan has changed to P0V3 and our Memory usage is already going down due to more Memory being added:

<img width="1564" height="705" alt="image" src="https://github.com/user-attachments/assets/35a7c709-aba8-4b80-93c8-dc1a3dac0c5e" />


*Azure scaling changes the SKU, not necessarily adding Memory or CPU cores individually.*

## Scale Out (More Servers/Instances)

Let's say we need to add more servers to handle more traffic, we can add more Server instances by Scaling Out.

Under our ASP, we'll go to **Settings > Scale up (App Service plan)**

### Scaling Methods

We can either set and keep our instances at a set number with Manual Scaling:

<img width="778" height="412" alt="image" src="https://github.com/user-attachments/assets/e6015a58-3166-4c8e-879b-4149de99cdc9" />

We can adjust scaling automatically with Auto Scaling

<img width="767" height="403" alt="image" src="https://github.com/user-attachments/assets/0a017594-71d3-479c-a6bb-da796b83fe45" />

Our instance number will stay at our default number, but will increase within the range of the Maximum number of instances:

<img width="767" height="403" alt="image" src="https://github.com/user-attachments/assets/55e4e63d-6a49-4278-a67e-94ee9ee467df" />

Under Rule Based, you can configure a custom scale rule that will scale based on set app metrics like CPU load:

<img width="1906" height="825" alt="image" src="https://github.com/user-attachments/assets/5d0ce784-d005-413a-b78f-1f52018e6652" />






