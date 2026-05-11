# Edit and Deploy an ARM Template

In this doc, we'll make changes to our newly downloaded ARM template.

## Edit Template

We'll search for 'Deploy a custom template' in the Azure Portal:

<img width="644" height="96" alt="image" src="https://github.com/user-attachments/assets/53bf8fcb-c6bb-4663-98bb-975c7df58a0d" />

We'll use the 'Build your own template' option:

<img width="1563" height="732" alt="image" src="https://github.com/user-attachments/assets/c64f8cf0-60b5-44d6-b6a1-266e7cf3f502" />

We'll click 'Load file' and select our recently downloaded ARM template:

<img width="1427" height="359" alt="image" src="https://github.com/user-attachments/assets/429f4c9d-b5fd-4c26-8e90-36043ac65812" />

Next, to deploy a copy of the Disk we created with our template, we'll need to change the name.

Here is the original template:

<img width="1288" height="543" alt="image" src="https://github.com/user-attachments/assets/7ddfc5fc-c224-4e46-91c5-5903bd3d9fc0" />

We'll change the name from 'disks_az104_disk1_name' to 'disk_name', 
and change the default value in our parameter to 'az104-disk2'

<img width="1684" height="932" alt="image" src="https://github.com/user-attachments/assets/9070f98b-c169-4ec0-9a1c-0a32285aa217" />

We'll click 'Save'

We also need to upload and edit the Parameters file. We'll click 'Edit parameters'

<img width="1028" height="618" alt="image" src="https://github.com/user-attachments/assets/37770d29-a2d1-43ae-afaa-4327b161a313" />

We'll change the parameter from 'disks_az104_disk1_name' to 'disk_name' here as well, and Save.

<img width="1176" height="482" alt="image" src="https://github.com/user-attachments/assets/d19dcd46-4936-41c7-8914-db1a6e817dc5" />

We can Review and Create.

We can see that Azure automatically sees the name of our Disk that we changed from the Template.

<img width="634" height="323" alt="image" src="https://github.com/user-attachments/assets/a542704a-6877-4af5-a7a5-70319967573a" />

Now in our Resource Group, we have our original Disk and our Template made Disk:

<img width="2543" height="724" alt="image" src="https://github.com/user-attachments/assets/4741fba8-ead5-4029-838d-14bfb2ee9706" />

