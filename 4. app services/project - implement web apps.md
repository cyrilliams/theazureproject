# Implement a Web App

In this doc, we'll create a Web App, configure it to display text from a GitHub repository. 
We'll also configure a Deployment Slot (CI/CD) and Autoscaling.

## Create a Web App

We'll go to 'App Services' in the Azure Portal:

<img width="186" height="52" alt="image" src="https://github.com/user-attachments/assets/b720ba2b-966e-4f6e-ab60-536c85e7d571" />

**Create > Web App**

<img width="292" height="227" alt="image" src="https://github.com/user-attachments/assets/7c4d558e-e9dd-4413-bf20-db7a4ec5b084" />

We'll create the Web App with the following settings:

<img width="935" height="1056" alt="image" src="https://github.com/user-attachments/assets/8b743d35-41c0-4ea3-91ff-253cc1d49476" />

We'll keep the default Pricing Plan options:

<img width="982" height="578" alt="image" src="https://github.com/user-attachments/assets/19003bef-3dce-4c35-8842-eb886e3cad1b" />

And Create:

*I did have to change the Location to Canada East due to storage quota limitations*

<img width="1815" height="483" alt="image" src="https://github.com/user-attachments/assets/58b0119b-7253-408e-92ab-fb04d4b098ca" />

## Deployment Slot

We'll first configure a Deployment Slot for us test and run our code, before releasing it out into the world.

In our Staging Slot, go to **Deployment > Deployment slots > Add slots**

We'll create the Slot name and Add:

<img width="712" height="278" alt="image" src="https://github.com/user-attachments/assets/b32fcb65-0abf-4525-ba8c-3256e9d20b2f" />

Now we have a Production and Staging Deployment Slots:

<img width="2220" height="296" alt="image" src="https://github.com/user-attachments/assets/032489de-8509-4065-9e50-cf2efdb5acaa" />


## Web App Deployment Settings

We'll go to **Deployment > Deployment center > External Git**

We'll use this repository: https://github.com/Azure-Samples/php-docs-hello-world
and the 'master' branch.

<img width="1391" height="836" alt="image" src="https://github.com/user-attachments/assets/b5f3bf44-3679-4a14-b2c1-520f44f50b21" />


We'll Save and then go to **Overview > Default domain**

And boom, we can see 'Hello World' when we click the Staging link:

<img width="1076" height="271" alt="image" src="https://github.com/user-attachments/assets/e0b412c1-5516-4479-af1e-e14e91eafa20" />

*This comes from the index.php file in the specified Repo*

<img width="602" height="344" alt="image" src="https://github.com/user-attachments/assets/edb414bd-7dd9-4ce4-81d5-9449642e1bf4" />


## Swap Deployment Slots

This is great but the code/app is not in Production. 

If I use the Production link, I get this:

<img width="1112" height="1034" alt="image" src="https://github.com/user-attachments/assets/ae8f3fd1-7a6c-4079-9f8f-dfd21ae43f68" />

Let's swap the Staging code to move to the Production code.

We'll go to our Web App, **Deployment > Deployment slots > Swap > Start Swap**

<img width="718" height="587" alt="image" src="https://github.com/user-attachments/assets/a03f70ce-b37f-46d8-a4f7-5466d9477b71" />



Now if we go use the Production link, it will give us this:

<img width="1030" height="287" alt="image" src="https://github.com/user-attachments/assets/f4e05100-a10e-4453-adf9-3fc9b742a1bc" />


*You can verify the links are the same here as well from the Microsoft error message earlier*

## Configure Auto Scaling


In this part, we'll configure Auto Scaling, which allows our Web App to automatically scale to meet performance needs.
In the real world, this would be useful for a company that receives more web traffic towards the Holidays.

We'll go to our Web App, **App Service plan > Scale out > Automatic**

<img width="996" height="398" alt="image" src="https://github.com/user-attachments/assets/d5069973-8042-4a99-93ef-eae1492e07fd" />

We'll increase the 'Maximum burst size' and 'Always ready instances' to 2 and Save.

<img width="1123" height="988" alt="image" src="https://github.com/user-attachments/assets/e1e97966-d4ae-4119-9731-06016b83aad6" />

## Test Load

To test and make sure our Web App can handle more traffic, we'll go to **Performance > Load Testing > Create test**

We'll create a new Load Testing Resource

<img width="724" height="571" alt="image" src="https://github.com/user-attachments/assets/6909acb9-cc10-4d3e-9709-508b5b3d8e0d" />

Under 'Add request', we'll specify our Web App (production) link:

<img width="1060" height="522" alt="image" src="https://github.com/user-attachments/assets/cf4c3a9b-116c-4aa2-adac-9fb8173d8532" />

We'll Review and Create, then navigate to the Test:

We can see the Test Metrics as well:

<img width="2552" height="1168" alt="image" src="https://github.com/user-attachments/assets/6b041ebc-2e95-4b79-9447-34e5f3e96874" />


