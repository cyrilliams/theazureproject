*3 of 3 from [Azure Storage Account LAB](https://github.com/cyrilliams/theazureproject/blob/main/LABS/lab%20-%20azure%20storage%20account.md)

# Create & Manage Azure File Share/Storage


Next, we'll create an Azure File share.


We'll go to our Storage Account, **Data storage > File shares > + File shares**


We'll give it a name:


<img width="984" height="335" alt="image" src="https://github.com/user-attachments/assets/cd4f2226-5e91-4a5f-be64-a91d1f3128ba" />




We can see that it uses Port 445, like a regular file share:


<img width="904" height="86" alt="image" src="https://github.com/user-attachments/assets/0ae374dd-90e9-4642-8fdc-9ed6163d78fe" />


Create the file share.


*There should be a section to review the Access tier but it did not show up for me this time*


Now we have a file share:


<img width="2542" height="1140" alt="image" src="https://github.com/user-attachments/assets/3a3f8954-b9b0-411c-a136-912bc1c8eaf9" />




I'll upload a picture using the Upload button:


<img width="720" height="607" alt="image" src="https://github.com/user-attachments/assets/95e00991-7c88-4e7b-b779-7e30ef5ac3df" />


If we click 'Browse', we can find our newly uploaded file:


<img width="2540" height="370" alt="image" src="https://github.com/user-attachments/assets/006d6587-f876-45f7-a561-1c31c91fa6fc" />


### Restrict Network Access


We may want to restrict who can access our file share. Lets do that by creating a VNet.


<img width="262" height="64" alt="image" src="https://github.com/user-attachments/assets/381c5c63-aa80-43e2-95cd-233514ed58ba" />


In the new VNet, we'll go to **Settings > Service endpoints > Add**, and configure the following Microsoft.Storage service endpoint:


<img width="535" height="556" alt="image" src="https://github.com/user-attachments/assets/b968628d-6cb8-4b46-8017-b0f3ea7b56f0" />


Add.


We'll go back to our Storage Account and go to 
**Security + networking > Networking > Public network access > Manage**


Under Virtual Networks, we'll add an existing VNet:


<img width="851" height="254" alt="image" src="https://github.com/user-attachments/assets/095c7b1a-31d7-4339-9217-3750120f3e8d" />


Select the appropriate Vnet and Subnet:


<img width="362" height="344" alt="image" src="https://github.com/user-attachments/assets/b0d08c0d-8964-4551-8d83-bd8a00adbb39" />




We can see it's been added:


<img width="2539" height="284" alt="image" src="https://github.com/user-attachments/assets/dd3932be-75b4-458f-b9f4-8473b9e2bba1" />


*For this test, we'll delete my machines public IP address so we can verify we cannot access the file*


Save.


Now if we go to **Storage browser > File shares**, and select our file, we get this error:


<img width="1192" height="711" alt="image" src="https://github.com/user-attachments/assets/4e3cc8e2-5a35-4ace-b80a-146fcb8a2867" />


*We can see that we are no longer authorized to perform this operation and it even recommends adding our IP address*


If we add our (Public) IP address back and retry, we are now able to access the file:


<img width="1715" height="615" alt="image" src="https://github.com/user-attachments/assets/e94d41a1-c45b-490a-b329-8ff9efaa5904" />


Now we have access to our file:


<img width="2555" height="1176" alt="image" src="https://github.com/user-attachments/assets/7bc3cb21-5be2-4e6a-b093-a6013942eb31" />
