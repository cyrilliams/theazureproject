# Azure File Sync

In this lab, we'll setup and configure Azure File Sync

## Create Storage Account - File Share

First, we'll create a Storage Account:

<img width="986" height="787" alt="image" src="https://github.com/user-attachments/assets/e8f10deb-83b1-44aa-9a44-c0a38d6a4043" />


Next, create a File Share:

<img width="884" height="516" alt="image" src="https://github.com/user-attachments/assets/098bc0e2-7559-490c-8aeb-4f126865270d" />


## Create + Configure Storage Sync Service

<img width="130" height="103" alt="image" src="https://github.com/user-attachments/assets/d2706a23-1d05-47bf-87da-75215e1edd3d" />

We'll click Create to create a Sync Service:

<img width="744" height="417" alt="image" src="https://github.com/user-attachments/assets/b1d6956f-f79d-4e46-ad63-a0fd1590193a" />


Next, we'll create a Sync Group:

In our Sync Service, go to **Sync > Sync groups > Create a sync group**

Select our Storage account and File Share:

<img width="614" height="497" alt="image" src="https://github.com/user-attachments/assets/9b610bd3-5371-4b1a-b658-fb9d0f47b98f" />


Create.

## Configure Windows Server and File Sync Agent

In this part, I'll use my existing Windows Server to test our File Sync.

### Disable Internet Explorer Enhanced Security

Per [Microsoft Learn](https://learn.microsoft.com/en-us/azure/storage/file-sync/file-sync-deployment-guide?tabs=azure-portal%2Cproactive-portal), we must disable Internet Explorer Enhanced Security.

In our Windows Server, go to **Local Server > Properties > IE Enhanced Security Configuration > Off**

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c8ba512f-78e1-49fd-a191-8f24d18c2063" />

### Install Azure CLI

We'll install Azure CLI from [Microsoft Learn](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?view=azure-cli-latest&pivots=msi)

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/4ea0453c-41bf-4111-afd6-4e104c58a70b" />

Then in PowerShell, run ```az login```

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/26031014-aae1-44c8-83a2-f0e78ef1d8cd" />

After logging in, you should get this:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2a8d035d-fac1-48f7-b13b-727e19b2b8ae" />


### File Sync Agent

Download the Azure File Sync Agent on the server:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/722c5356-6fc9-4fb9-b7a7-7c56edfc7bf2" />


Once it installs, we'll sign into the Agent:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b59335d7-d617-4e73-8a98-224345478927" />

Select the correct Subscription, Resource Group and Sync Service:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/7e655b2c-5020-43f2-a981-b0082ab1bf61" />

Register.

### Create File Share

Next, we'll create a Folder to use as the File Share endpoint. I'll use ```C:\Shares\AZ104-FileSync```

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/3c082dba-d6f8-408c-99b5-dd7eb98967fa" />


### Create Server Endpoint

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/247979f6-61f3-4db1-a38b-1f9f81292541" />

Now, I'll go back into Azure Portal, go to my Sync Group, then 'Add server endpoint'

<img width="571" height="575" alt="image" src="https://github.com/user-attachments/assets/31debe93-e02d-4acc-946a-6c6a2c9622d0" />


Create.

We now have our Server Endpoint. It will start initializing.

<img width="1672" height="229" alt="image" src="https://github.com/user-attachments/assets/b0150350-d8fb-441e-b516-8a05399d7f80" />


### Optional - Cloud Tiering

We can also enable Cloud Tiering, which allows files to be saved only to Azure if they are not frequently accessed. 
This method frees up space for Servers who have a lot of infrequently accessed files.


Select the Server Endpoint, then go to **Settings > Cloud tiering settings > Enable cloud tiering** 
or Enable it when you configure the Server Endpoint.


<img width="1188" height="661" alt="image" src="https://github.com/user-attachments/assets/00ca942f-0bd2-4be2-892b-106a6169d490" />


Save.


## Verify Sync

File Sync works by syncing from Azure File Shares to your on Prem Servers.

Let's verify this is working by adding a file to the File Share.

First, verify there is nothing in the on Prem server:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/509a3f71-8919-48c1-a69e-dafd74a54465" />

We'll now go to our File Share, **Browse > Upload**

<img width="1903" height="381" alt="image" src="https://github.com/user-attachments/assets/1a62fc73-f6b5-4291-992d-24f63df77359" />


Now we have one file in our File Share:

<img width="1905" height="403" alt="image" src="https://github.com/user-attachments/assets/52ac185e-aaa0-425b-a359-00827c7b1eda" />

### Invoke Storage Sync Change Detection

Azure does detects changes every 24 hours. 
If we want to verify a change has synced faster than that, we'll need to run
```Invoke-AzStorageSyncChangeDetection```

To do this, you'll need to install the Az Module on the Server with:
```Install-Module -Name Az -Repository PSGallery -Force```

Restart PowerShell and run ```Connect-AzAccount``` to confirm changes:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c01fb019-df21-4a26-bfc3-27d2469b56ee" />

This is the full command I used:

```
Invoke-AzStorageSyncChangeDetection -ResourceGroupName "filesync-rg" -StorageSyncServiceName "az104syncservice" -SyncGroupName "az104syncgroup" -CloudEndpointName "aae0d1fd-c199-4ffd-9e8a-93cdf6dc02ef"
```

*To get your Cloud Endpoint name, run: ```Get-AzStorageSyncCloudEndpoint```*

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/8ccc5e3e-7402-4c2a-adbf-20ff4b61dfe9" />


### Verify

Let's check our on Prem server now:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/3b851f80-38da-4451-bd73-231aed27cee8" />


### Verify Again

The last part took me a while to get so I want to verify that the ```Invoke-AzStorageSyncChangeDetection``` works instantly.

I'll add the Skrillex song to my File Share:

<img width="1912" height="411" alt="image" src="https://github.com/user-attachments/assets/0321b8b4-6a7a-4f8e-bf61-00c6a143e8cc" />

Verify there song isn't there yet:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b0529979-6c1a-4ff6-8d06-9f278622ed6f" />

I'll run my Invoke command one more time:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/2bfaf3b5-b409-47fc-ae59-c75a7bbe4b58" />

Boom:

<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/4a97c92b-b5a7-44c8-a75e-77eadf1a611f" />
