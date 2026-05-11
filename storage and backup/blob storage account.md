*2 of 3 from [Azure Storage Account LAB](https://github.com/cyrilliams/theazureproject/blob/main/LABS/lab%20-%20azure%20storage%20account.md)*

# Blob Storage

Blob storage is a great tool to use to access a file without having to go through a traditional file share or file in a directory or hard drive.

To access the file, Azure simply serves you a web url that you can access or give someone else to access, rather than having to configure setting up credentials to access a server or file share.

Lets set this up now:

Under **Data storage > Containers > Add container**

<img width="531" height="454" alt="image" src="https://github.com/user-attachments/assets/57cc7e91-9ddb-4771-a942-920053737f7f" />

Create.

### Immutable Blob Storage

To make sure the Blob Container stays in an immutable state, we'll click the '...' on our Blob, 
then **Access Policy > Immutable blob storage > Add policy**

We'll change to 'Time-based retention' and set the retention period to 180 days:

<img width="720" height="507" alt="image" src="https://github.com/user-attachments/assets/c20f0bed-78b5-43ca-8abe-15951fdf3259" />

Save.

This will keep data from being deleted for that set duration.

## Manage Blob Container

We'll first upload a file into our Blob Container.

We'll click our Storage account, then click Upload.

We can upload a file here:

<img width="714" height="336" alt="image" src="https://github.com/user-attachments/assets/b2e80cb5-907c-488d-84b2-cb5ecc85fb94" />

And we have Advanced options to go along with the upload, such as Access tier, upload folder, and the retention policy (if we did not set it earlier)

<img width="712" height="852" alt="image" src="https://github.com/user-attachments/assets/21553711-6cb5-452c-9f4f-e941286f2ef1" />


Upload a file and click Upload.

We can see that it uploaded our file and created a Directory. I set this in the Upload folder (not shown in the last picture)

<img width="2215" height="379" alt="image" src="https://github.com/user-attachments/assets/59b25c79-01a5-4ab5-befc-bb7ca5410f79" />


Now, we can see our file and it's info:

<img width="2207" height="396" alt="image" src="https://github.com/user-attachments/assets/49f9c815-44ef-4252-be0b-11f46ad8d8b6" />



We can click the file and get the URL:

<img width="1383" height="1116" alt="image" src="https://github.com/user-attachments/assets/825d6428-741e-44a1-9f41-db21552987bf" />

Let's copy and paste it in our browser:

<img width="1498" height="360" alt="image" src="https://github.com/user-attachments/assets/dea00d62-eefd-400f-aaa5-45f1936f0873" />

We get this error stating that public access is not permitted. Let's change this.

### Configure Limited Access

We'll configure limited access using a Shared Access Signature

We'll right click our file and click the '...', then click 'Generate SAS'

<img width="228" height="588" alt="image" src="https://github.com/user-attachments/assets/b62827e7-76d2-41e4-ac70-95bac03b011b" />


This allows us to configure and set the Policies around what type of access is given and for how long:

<img width="715" height="959" alt="image" src="https://github.com/user-attachments/assets/4c53ee53-3870-4751-a3da-39694e7b59bf" />

We'll click 'Generate SAS token and URL'

It gives us our Token and URL here:

<img width="716" height="168" alt="image" src="https://github.com/user-attachments/assets/37bd5887-368d-4524-838e-54000a3be4dc" />



Now, if we enter that URL into our browser:

<img width="2560" height="1380" alt="image" src="https://github.com/user-attachments/assets/e25fa2ea-c35a-4160-8e58-b45c24515245" />

BOOM, we now have access!
