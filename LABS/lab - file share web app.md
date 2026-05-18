# ShareSafely - File Share Web App

In this lab, we'll create an File Sharing Web App that stores files with Azure Blob Storage,
gives the user a URL that ensures only authorized users have access to it and for a limited time.

## Create Resource Group

We'll use the Cloud CLI (PowerShell) to create our Resource Group:

Run ```new-AzResourceGroup -Name sharesafely-rg -Location eastus```

We get:
```
ResourceGroupName : sharesafely-rg
Location          : eastus
ProvisioningState : Succeeded
Tags              : 
ResourceId        : /subscriptions/[id]/resourceGroups/sharesafely-rg
```
<img width="1268" height="263" alt="image" src="https://github.com/user-attachments/assets/332855f8-ccf0-46cb-b56d-4f2e4de1d41c" />

## Create Storage Account

We'll run:
```
new-AzStorageAccount -ResourceGroupName sharesafely-rg -Name sharesafelystorageacc -Location eastus -SkuName Standard_LRS -Kind StorageV2
```
and we'll get:
```
StorageAccountName    ResourceGroupName PrimaryLocation SkuName      Kind      AccessTier CreationTime         ProvisioningState EnableHttpsTrafficOnly LargeFileShares
------------------    ----------------- --------------- -------      ----      ---------- ------------         ----------------- ---------------------- ---------------
sharesafelystorageacc sharesafely-rg    eastus          Standard_LRS StorageV2 Hot        5/18/2026 3:09:09 AM Succeeded         True                   
```

## Create Blob Container

Now we need a Blob Container to put our files in.

First we'll create the Storage Account Context, then the Container.

*An Azure Storage Context is a configuration object in Azure PowerShell used to securely authenticate and define the specific storage account you are managing. 
It holds the account name, access keys or connection strings, and subscription details so you can run storage commands without re-entering your credentials*

Run:
```
PS /home/cyril> $context = New-AzStorageContext -StorageAccountName sharesafelystorageacc -UseConnectedAccount                                              
PS /home/cyril> New-AzStorageContainer -Name "uploads-blob" -Context $context
```
And we get:
```
Name                 PublicAccess         LastModified                   IsDeleted  VersionId
----                 ------------         ------------                   ---------  ---------
uploads-blob         Off                  5/18/2026 3:15:56 AM +00:00               
```
<img width="1136" height="198" alt="image" src="https://github.com/user-attachments/assets/27b3e16b-8d56-46de-bc2e-73fa51871546" />


## Create Azure Key Vault

We'll run:
```
new-azkeyVault -Location eastus -Name sharesafely-keyvault -ResourceGroupName sharesafely-rg
```
And we get:

<img width="2219" height="683" alt="image" src="https://github.com/user-attachments/assets/f852225b-5e98-490c-b166-109cb8779cb7" />

## Get & Store Storage Account Connection String

We'll get the Storage Account Connection String needed for the Web App.

Run ```$secret = (Get-AzStorageAccount -ResourceGroupName sharesafely-rg -Name sharesafelystorageacc).Context.ConnectionString```
in a variable for the next step.

We'll get this Connection String:

```
BlobEndpoint=https://sharesafelystorageacc.blob.core.windows.net/;QueueEndpoint=https://sharesafelystorageacc.queue.core.windows.net/;TableEndpoint=https://sharesafelystorageacc.table.core.windows.net/;FileEndpoint=https://sharesafelystorageacc.file.core.windows.net/;AccountName=sharesafelystorageacc;AccountKey=jvsWfSlNLmtk8H9FdUjZgLwH60F2mvi21Y20Mc/1oCElCEbAockeS0iGuY31m+pNnfcLy5rzwI2X+ASt8+Hpwg==
```
*We want to keep this safe. I'll delete this after the lab is done*

A storage account connection string is a secure text containing all the necessary information 
(account name, account key, and service endpoints) required for an application to programmatically 
authenticate and access data in cloud storage (such as Azure Storage).

*Do not hard code Connection Strings*

We'll store it in our Key Vault by running a few commands.

First we need to conver the variable to Secure String with:
```
$secret = ConvertTo-SecureString -String "BlobEndpoint=https://sharesafelystorageacc.blob.core.windows.net/;QueueEndpoint=https://sharesafelystorageacc.queue.core.windows.net/;TableEndpoint=https://sharesafelystorageacc.table.core.windows.net/;FileEndpoint=https://sharesafelystorageacc.file.core.windows.net/;AccountName=sharesafelystorageacc;AccountKey=jvsWfSlNLmtk8H9FdUjZgLwH60F2mvi21Y20Mc/1oCElCEbAockeS0iGuY31m+pNnfcLy5rzwI2X+ASt8+Hpwg==" -AsPlainText -Force
```


Next, we'll store the Connection into our Key Vault with:
```
Set-AzKeyVaultSecret -Name ss-storageconnection -SecretValue $secret -VaultName sharesafely-keyvault
```
We'll get this output:
```
Vault Name   : sharesafely-keyvault
Name         : ss-storageconnection
Version      : fed8e619e8504eca88b18ac68d2830c1
Id           : https://sharesafely-keyvault.vault.azure.net:443/secrets/ss-storageconnection/fed8e619e8504eca88b18ac68d2830c1
Enabled      : True
Expires      : 
Not Before   : 
Created      : 5/18/2026 3:33:05 AM
Updated      : 5/18/2026 3:33:05 AM
Content Type : 
Tags         : 
```
If we look in our Portal, we have our two resources:

<img width="1819" height="634" alt="image" src="https://github.com/user-attachments/assets/3a37aa9f-fb10-4b48-b441-c9b77254b307" />

If we look in our Key Vault, under Secrets, we'll find our Context Connection String:

<img width="2546" height="638" alt="image" src="https://github.com/user-attachments/assets/d325584a-1af0-4746-98ce-cb2718f5af4d" />







# Create Web App

Now we'll create the Web App!

We'll need to install the following:
- Node.js
- Azure CLI
- Node Package Manager (NPM)

## Create Server

To host our app, I'll quickly create an Ubuntu Server in Azure Portal:

<img width="1031" height="1055" alt="image" src="https://github.com/user-attachments/assets/287e6dcc-5506-4a14-99a8-aee49e94a00e" />

I'll also use a Key Pair that I am not longer using:

<img width="958" height="848" alt="image" src="https://github.com/user-attachments/assets/2bf16376-c230-4c10-aa9c-861b28f5017a" />

I'll let Azure create my Vnet and Subnet:

<img width="1096" height="920" alt="image" src="https://github.com/user-attachments/assets/a61c26dc-4188-4061-9055-2331b5b62ae2" />


After it's created, we'll remote in using our Private Key:

<img width="1074" height="827" alt="image" src="https://github.com/user-attachments/assets/e3c16e96-d76c-4f62-8937-68ca209685f4" />

After we'll run: ```sudo apt update && sudo apt upgrade```

## Allow Port

We'll use Port 3000 for the Web Server. 

I'll add it to our Network Security Group:

<img width="2200" height="472" alt="image" src="https://github.com/user-attachments/assets/36692702-ecd9-4b06-ad38-e420ae6f647c" />


## Install Dependencies and Create Folders

First, we'll create a folder for our Web App code to go into, then go into that folder:

```bash
sudo mkdir -p /home/cyril/projects/ShareSafely
cd /home/cyril/projects/ShareSafely
```

Next, we'll install NPM with:
```
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

Verify the installation with:
```
node -v
npm -v
```
<img width="1144" height="155" alt="image" src="https://github.com/user-attachments/assets/0837d270-a5d8-4c87-b68f-9a69c34ffbf5" />

We'll then install the NPM packages by running:
```
sudo npm install express multer dotenv
sudo npm install @azure/storage-blob
sudo npm install @azure/keyvault-secrets
sudo npm install @azure/identity
```

```md
**What Each Package Does**
Package	Purpose
express	Web server framework
multer	Handles file uploads
dotenv	Reads .env variables
@azure/storage-blob	Azure Blob Storage SDK
@azure/keyvault-secrets	Access Key Vault secrets
@azure/identity	Azure authentication
```

## Install Azure CLI

We'll run:
```
sudo curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```
Verify with:
```az version```

## Create Supporting Folders

We'll need to create the following file & folder structure:
```
ShareSafely/
│
├── server.js
├── .env
├── package.json
│
├── uploads/
│
└── views/
    └── index.html
```

We'll run:
```bash
sudo mkdir uploads views
ls # to list files and directories
```

### HTML File

We'll ```cd``` into our ```views``` folder and create an HTML index file:

I'll run: ```sudo nano index.html``` and copy my code:
```html
<!DOCTYPE html>
<html>
<head>
    <title>ShareSafely</title>
</head>
<body>

<h1>Upload File</h1>

<form action="/upload" method="post" enctype="multipart/form-data">
    <input type="file" name="file" />
    <button type="submit">Upload</button>
</form>

</body>
</html>
```
*ChatGPT did write this for me*

## JavaScript File

I'll create our Server JavaScript file using ```sudo nano server.js```

Copy our code from ChatGPT into our text editor:
```.js
require('dotenv').config();

const express = require('express');
const multer = require('multer');
const fs = require('fs');
if (!fs.existsSync('uploads')) {
    fs.mkdirSync('uploads');
}
const {
    BlobServiceClient,
    StorageSharedKeyCredential,
    generateBlobSASQueryParameters,
    BlobSASPermissions
} = require('@azure/storage-blob');

const app = express();
const upload = multer({ dest: 'uploads/' });

app.use(express.static('views'));

const connectionString = process.env.AZURE_STORAGE_CONNECTION_STRING;
const containerName = 'uploads-blob';

const blobServiceClient =
    BlobServiceClient.fromConnectionString(connectionString);

app.post('/upload', upload.single('file'), async (req, res) => {

    const file = req.file;

    const containerClient =
        blobServiceClient.getContainerClient(containerName);

    const blobClient =
        containerClient.getBlockBlobClient(file.originalname);

    await blobClient.uploadFile(file.path);

    // Generate SAS URL

    const accountName =
        blobServiceClient.accountName;

    const accountKey =
        process.env.AZURE_STORAGE_KEY;

    const sharedKeyCredential =
        new StorageSharedKeyCredential(
            accountName,
            accountKey
        );

    const expiresOn = new Date(
        new Date().valueOf() + 3600 * 1000
    );

    const sasToken = generateBlobSASQueryParameters(
        {
            containerName,
            blobName: file.originalname,
            permissions: BlobSASPermissions.parse("r"),
            expiresOn
        },
        sharedKeyCredential
    ).toString();

    const sasUrl =
        `${blobClient.url}?${sasToken}`;

    fs.unlinkSync(file.path);

    res.send(`
        <h2>File Uploaded</h2>
        <p>Share this link:</p>
        <a href="${sasUrl}">
            ${sasUrl}
        </a>
    `);
});

app.listen(3000, () => {
    console.log('Server running on port 3000');
});
```

## Environment Variable

I'll create our Environment Variable by running:
```sudo nano .env```
I'll copy our Env. Variable in:
```
AZURE_STORAGE_CONNECTION_STRING=YOUR_CONNECTION_STRING
AZURE_STORAGE_KEY=YOUR_STORAGE_KEY

# Mine looks like:

AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=sharesafelystorageacc;AccountKey=jvsWfSlNLmtk8H9FdUjZgLwH60F2mvi21Y20Mc/1oCElCEbAockeS0iGuY31m+pNnfcLy5rzwI2X+ASt8+Hpwg==;BlobEndpoint=https://sharesafelystorageacc.blob.core.windows.net/;FileEndpoint=https://sharesafelystorageacc.file.core.windows.net/;QueueEndpoint=https://sharesafelystorageacc.queue.core.windows.net/;TableEndpoint=https://sharesafelystorageacc.table.core.windows.net/"

AZURE_STORAGE_KEY="jvsWfSlNLmtk8H9FdUjZgLwH60F2mvi21Y20Mc/1oCElCEbAockeS0iGuY31m+pNnfcLy5rzwI2X+ASt8+Hpwg=="

# Do not store these or post these to the Public. I will be deleting this after
```

## Get Storage Account Key

Next, we'll get the Storage Account Key.

First we'll need to use ```az login``` to authenticate with our Azure account.

It has us use a link and enter a code:

<img width="544" height="456" alt="image" src="https://github.com/user-attachments/assets/06bfe3b8-360b-4379-a1f3-880ebdba3563" />

Now we are authenticated:

<img width="1883" height="439" alt="image" src="https://github.com/user-attachments/assets/d31652cc-e168-4a3e-910c-e13cd6ca192c" />

We'll run:
```
az storage account keys list --account-name sharesafelystorageacc --resource-group sharesafely-rg
```
Which gives us the Storage Account Key:
```
[
  {
    "creationTime": "2026-05-18T03:09:10.453455+00:00",
    "keyName": "key1",
    "permissions": "FULL",
    "value": "[Taken Out]"
  },
  {
    "creationTime": "2026-05-18T03:09:10.453455+00:00",
    "keyName": "key2",
    "permissions": "FULL",
    "value": "[Taken Out]"
  }
]
```
<img width="1900" height="492" alt="image" src="https://github.com/user-attachments/assets/f58ba7b7-e5c2-4b12-996c-5f29e4b59278" />


## Run App

We'll use ```node server.js``` to start our application:

We should see: ```Server running on port 3000```

<img width="1196" height="108" alt="image" src="https://github.com/user-attachments/assets/85e6a134-8e0f-4af7-9e1c-0bde02facba2" />

Let's get to it from a Web Browser:.

```http://52.146.18.200:3000/```

Now we get:

<img width="2558" height="608" alt="image" src="https://github.com/user-attachments/assets/971b4799-a2a3-44d0-a5d0-4991e116ab44" />


## Try Out App

Let's Upload something. I'll click Browse:

<img width="1224" height="1036" alt="image" src="https://github.com/user-attachments/assets/93ed3d7a-eeb2-420c-b48c-ca95f47890f8" />

*After fixing a folder permission issue with 
```sudo chmod 777 uploads``` and
```sudo chown -R azureuser:azureuser uploads```, 
we get:*

<img width="2108" height="224" alt="image" src="https://github.com/user-attachments/assets/15d153aa-5193-41aa-90c0-e9cad7f5e9f8" />

Let's click the Link:

<img width="544" height="84" alt="image" src="https://github.com/user-attachments/assets/53d1c5a9-0e6c-45bd-96f9-b986706c5470" />

It downloads for us! Amazing!


## Verify in Blob Container

If we go into our Container, we can find our uploaded File:

<img width="2547" height="519" alt="image" src="https://github.com/user-attachments/assets/e9318f1c-e545-466b-8da0-1523593e3165" />





