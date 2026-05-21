# AzCopy

AzCopy is used to trasnfer data from on premise storage sources like a Windows Server to your Azure Blob and File accounts.
It can also be used to transfer the opposite way, from Blob and File accounts to on prem storage sources.
It can also copy data from storage account to storage account.

In this doc, we will be using AzCopy and learn the fundamentals of how it works and it's use cases.

## Create Resources

First, we'll login in PowerShell by running ```Connect-AzAccount```, then going through the sign in prompts.

<img width="1256" height="721" alt="image" src="https://github.com/user-attachments/assets/ff292269-ede4-4a9d-9cce-a6e25ac1ed57" />

### Resource Group

We'll create our Resources Group:
```powershell
PS C:\> New-AzResourceGroup -Name AzCopyLab-rg -Location "eastus"

ResourceGroupName : AzCopyLab-rg
Location          : eastus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/[id]/resourceGroups/AzCopyLab-rg
```
### Storage Account

Next, create the Storage Account:
```powershell
PS C:\> New-AzStorageAccount -ResourceGroupName AzCopyLab-rg -Name cyrilazcopystoracc -Location EastUs -SkuName "Standard_LRS" -Kind "StorageV2"


StorageAccountName ResourceGroupName PrimaryLocation SkuName      Kind      AccessTier CreationTime         ProvisioningState EnableHttpsTrafficOn
                                                                                                                              ly
------------------ ----------------- --------------- -------      ----      ---------- ------------         ----------------- --------------------
cyrilazcopystoracc AzCopyLab-rg      eastus          Standard_LRS StorageV2 Hot        5/21/2026 4:16:37 PM Succeeded         True

```

We can verify it in the Portal here:

<img width="1336" height="509" alt="image" src="https://github.com/user-attachments/assets/3a152c6a-0032-4d18-8aaa-23cdfb5a3d77" />

### Storage Container

We'll create our Storage Container within the Storage Account. 
First, we will need to create a Storage Context for the Container 

*A Storage Context tells Azure which Storage Account the Container will go into, what Authentication it will use, and it's Permissions*

```powershell
$context = New-AzStorageContext -StorageAccountName "cyrilazcopystoracc" -UseConnectedAccount
```
We specified the Storage Account we'll use and the authentication which is through my Azure account. 
We put that information into a variable.

After, we'll create the Container:
```powershell
PS C:\> New-AzStorageContainer -Name "azcopylabcontainer" -Context $context -Permission Off

   Storage Account Name: cyrilazcopystoracc

Name                 PublicAccess         LastModified                   IsDeleted  VersionId
----                 ------------         ------------                   ---------  ---------
azcopylabcontainer   Off                  5/21/2026 4:56:52 PM +00:00
```
We can verify it in the Portal as well:

<img width="1909" height="451" alt="image" src="https://github.com/user-attachments/assets/201174c3-a930-45dc-b0c4-d2c175088642" />

### Get Container URL

We'll want the URL for our Container for AzCopy. Let's get it:

Put the Get-AzStorageContainer information in a variable. I'll use ```$container```
```powershell
PS C:\> $container = Get-AzStorageContainer -Name "azcopylabcontainer" -Context $context
```
Then filter and return the Uri:
```powershell
PS C:\> $container.cloudBlobContainer.Uri.AbsoluteUri
https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer
```
I'll save that that in its own variable:
```powershell
PS C:\> $containerURL = $container.cloudBlobContainer.Uri.AbsoluteUri
PS C:\> Write-Host = $containerURL
= https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer
```

### View Container Contents

*You will need to ensure you have the Storage Blob Data Contributor role. Once assigned, Disconnect Azure Account and Re-Connect*

<img width="1277" height="390" alt="image" src="https://github.com/user-attachments/assets/dfe18713-f67b-48e4-9ff8-7ef1d7a9b238" />

If you still have the same PowerShell session that you built the context variable in, run:
```
Get-AzStorageBlob -Container "azcopylabcontainer" -Context $context
```
*If not context variable, rebuild it*

That command should return nothing.


Now, let's install and set up AzCopy


## AzCopy - On Prem to Azure

We can verify that AzCopy is not installed by running ```AzCopy --version```

<img width="1063" height="93" alt="image" src="https://github.com/user-attachments/assets/d099b27c-639d-4290-a9ea-16809cbe876c" />

### Download AzCopy

Next, we'll get the AzCopy from the [Microsoft Learn](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10) website:

<img width="756" height="339" alt="image" src="https://github.com/user-attachments/assets/559f4fde-83b0-485a-a1dc-01efc875cfbd" />

### Copy AzCopy.exe


We'll copy the extracted ```azcopy.exe``` file over to the C:\ drive:
*as admin*

```PS C:\Users\cwilliams> Copy-Item -Path "C:\Users\cwilliams\Downloads\azcopy_windows_amd64_10.32.4\azcopy_windows_amd64_10.32.4\azcopy.exe" -Destination "C:\AzCopy\"```

Now we can check to see if it moved by running:
```powershell
PS C:\Users\cwilliams> ls "C:\AzCopy\"
```
And we get:
```powershell
    Directory: C:\AzCopy

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---           5/21/2026 11:35 AM       60792672 azcopy.exe

```

### Verify AzCopy

*Switched to Command Prompt*

Now, use the ```cd``` command to change directories to wherever you put your file, and verify it with ```azcopy --version```:
```powershell
C:\Windows\System32>cd C:\

C:\>azcopy --version
azcopy version 10.32.4

C:\>
```

<img width="534" height="201" alt="image" src="https://github.com/user-attachments/assets/144e942d-7970-41ba-98c7-720c7d3be370" />


## Create Test Directory and Files

We'll quickly create a test Directory that we want to store all of our files in.
```powershell
C:\>mkdir C:\AzCopyLab
```

I'll copy some files over there and verify them:
```powershell
C:\>dir C:\AzCopyLab
 Volume in drive C is OS
 Volume Serial Number is F6D6-8383

 Directory of C:\AzCopyLab

05/21/2026  12:04 PM    <DIR>          .
04/10/2025  03:39 PM            43,314 image (1).png
05/19/2025  08:55 AM           283,341 Image (2).png
03/27/2025  02:00 PM            36,796 image (3).jpg
               3 File(s)        363,451 bytes
               1 Dir(s)  228,960,145,408 bytes free
```


<img width="457" height="247" alt="image" src="https://github.com/user-attachments/assets/077be8f5-3681-452f-9b81-f2966fec272d" />

## Authenticate AzCopy

Next we'll authenticate our AzCopy by running ```azcopy login```

I'll have us enter a code in a provided link:

<img width="1127" height="602" alt="image" src="https://github.com/user-attachments/assets/1de3abf9-97ee-4fba-8b49-17194c620221" />

<img width="437" height="336" alt="image" src="https://github.com/user-attachments/assets/08c5fcbb-7249-470a-868f-245d8b8b3e42" />

### Use AzCopy - Copy Files in Directory

Now we'll run  
```powershell
C:\>azcopy copy "C:\AzCopyLab" "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer" --recursive
```
We'll get a confirmation message stating how many files were transferred:

<img width="1127" height="602" alt="image" src="https://github.com/user-attachments/assets/23a68696-d667-43e4-9356-38db47710781" />

Back in PowerShell, re-run our command to view Container contents:
```powershell
PS C:\> Get-AzStorageBlob -Container "azcopylabcontainer" -Context $context

   AccountName: cyrilazcopystoracc, ContainerName: azcopylabcontainer

Name                 BlobType  Length          ContentType                    LastModified         AccessTier SnapshotTime                 IsDeleted  VersionId
----                 --------  ------          -----------                    ------------         ---------- ------------                 ---------  ---------
AzCopyLab/Image (2)… BlockBlob 283341          image/png                      2026-05-21 17:26:59Z Hot                                     False
AzCopyLab/image (1)… BlockBlob 43314           image/png                      2026-05-21 17:26:59Z Hot                                     False
AzCopyLab/image (3)… BlockBlob 36796           image/jpeg                     2026-05-21 17:26:59Z Hot                                     False

PS C:\>
```
<img width="1490" height="262" alt="image" src="https://github.com/user-attachments/assets/c97ff8af-041b-497f-96eb-07118d69f698" />

Nice!

### Use AzCopy - Copy Single File

This one is even easier. We'll run:
```powershell
C:\>azcopy copy "C:\AzCopyLab\02 - Scary Monsters and Nice Sprites.mp3" "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer/AzCopyLab/"
```
<img width="1474" height="524" alt="image" src="https://github.com/user-attachments/assets/b0016482-59ed-42ad-939a-289e0bd4ecf4" />


### Verify AzCopy in Portal

Let's check the Portal:

<img width="1910" height="515" alt="image" src="https://github.com/user-attachments/assets/c047509e-fea3-4a3d-aed5-d6b73c169f58" />

Amazing!







## AzCopy - Download

Let's create a Download folder and verify:

```powershell
C:\>mkdir "C:\AzCopyLab\Downloads"
```
Verify with:
```powershell
C:\>dir "C:\AzCopyLab\"
 Volume in drive C is OS
 Volume Serial Number is F6D6-8383

 Directory of C:\AzCopyLab

05/21/2026  01:55 PM    <DIR>          .
04/21/2026  11:23 AM         8,207,365 02 - Scary Monsters and Nice Sprites.mp3
05/21/2026  01:55 PM    <DIR>          Downloads
04/10/2025  03:39 PM            43,314 image (1).png
05/19/2025  08:55 AM           283,341 Image (2).png
03/27/2025  02:00 PM            36,796 image (3).jpg
               4 File(s)      8,570,816 bytes
               2 Dir(s)  228,300,406,784 bytes free
```

Verify nothing is in the new folder :
```powershell
C:\>dir "C:\AzCopyLab\Downloads"
 Volume in drive C is OS
 Volume Serial Number is F6D6-8383

 Directory of C:\AzCopyLab\Downloads

05/21/2026  01:55 PM    <DIR>          .
05/21/2026  01:55 PM    <DIR>          ..
               0 File(s)              0 bytes
               2 Dir(s)  228,299,739,136 bytes free
```

### AzCopy - On Prem to Azure

In our Container, I've uploaded a new file:

<img width="1331" height="711" alt="image" src="https://github.com/user-attachments/assets/d8a5a3dc-c0bf-4175-a7a1-7e630c2fcd59" />

Now we'll run this and specify our File in Azure and the Download path:
```powershell
C:\>azcopy copy "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer/AzCopyLab/azure-a(1).png" "C:\AzCopyLab\Downloads"
```

<img width="1093" height="520" alt="image" src="https://github.com/user-attachments/assets/cb7a0ca9-9698-4ff1-a84a-07992bea593a" />

We can see one file has been transferred. Let's verify with an ```dir``` command:

```powershell
C:\>dir "C:\AzCopyLab\Downloads"
 Volume in drive C is OS
 Volume Serial Number is F6D6-8383

 Directory of C:\AzCopyLab\Downloads

05/21/2026  02:01 PM    <DIR>          .
05/21/2026  01:55 PM    <DIR>          ..
05/21/2026  02:01 PM            57,644 azure-a(1).png
               1 File(s)         57,644 bytes
               2 Dir(s)  228,292,657,152 bytes free
```

We can also see it is the same image in File Explorer:

<img width="685" height="327" alt="image" src="https://github.com/user-attachments/assets/2e850187-4e48-4944-88db-cd4e52ab473b" />



### Multiple Files

To copy/download multiples files but not the folder, we'll add '*' at the end of our file path:
```poweershell
C:\>azcopy copy "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer/AzCopyLab/*" "C:\AzCopyLab\Downloads"
```
If you look closely, you can see it tranferred 5 files, but 0 folders.

<img width="1153" height="498" alt="image" src="https://github.com/user-attachments/assets/8643d4a6-21c7-42e5-aca3-77f4f70553a0" />


Now we can see that we have more files in the Downloads folder:

```powershell
C:\>dir "C:\AzCopyLab\Downloads"
 Volume in drive C is OS
 Volume Serial Number is F6D6-8383

 Directory of C:\AzCopyLab\Downloads

05/21/2026  02:05 PM    <DIR>          .
05/21/2026  01:55 PM    <DIR>          ..
05/21/2026  02:05 PM         8,207,365 02 - Scary Monsters and Nice Sprites.mp3
05/21/2026  02:05 PM            57,644 azure-a(1).png
05/21/2026  02:05 PM            43,314 image (1).png
05/21/2026  02:05 PM           283,341 Image (2).png
05/21/2026  02:05 PM            36,796 image (3).jpg
               5 File(s)      8,628,460 bytes
               2 Dir(s)  227,294,916,608 bytes free
```


### Extras

AzCopy also has a couple other commands. You can see them if you run ```azcopy help```
```
Available Commands:
  bench          Performs a performance benchmark
  completion     Generate the autocompletion script for the specified shell
  copy           Copies source data to a destination location
  doc            Generates documentation for the tool in Markdown format
  env            Shows the environment variables that you can use to configure the behavior of AzCopy.
  help           Help about any command
  jobs           Sub-commands related to managing jobs
  list           List the entities in a given resource
  login          Log in to Microsoft Entra ID to access Azure Storage resources.
  logout         Log out to terminate access to Azure Storage resources.
  make           Create a container or file share.
  remove         Delete blobs or files from an Azure storage account
  set-properties Given a location, change all the valid system properties of that storage (blob or file)
  sync           Replicate source to the destination location
```


For instance, we can list the contents our Azure Container with:
```powershell
C:\>azcopy list  "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer"

INFO: Autologin not specified.
INFO: Authenticating to source using Azure AD
AzCopyLab/02 - Scary Monsters and Nice Sprites.mp3; Content Length: 7.83 MiB
AzCopyLab/Image (2).png; Content Length: 276.70 KiB
AzCopyLab/azure-a(1).png; Content Length: 56.29 KiB
AzCopyLab/image (1).png; Content Length: 42.30 KiB
AzCopyLab/image (3).jpg; Content Length: 35.93 KiB
```






## Blob to Blob File Transfer

We'll test out Blob to Blob file transer with AzCopy

I'll quickly create another Container:
```powershell
PS C:\Users\cwilliams> $context = New-AzStorageContext -StorageAccountName "cyrilazcopystoracc" -UseConnectedAccount
PS C:\Users\cwilliams> New-AzStorageContainer -Name "azcopylabcontainer2" -Context $context -Permission Off

   Storage Account Name: cyrilazcopystoracc

Name                 PublicAccess         LastModified                   IsDeleted  VersionId
----                 ------------         ------------                   ---------  ---------
azcopylabcontainer2  Off                  5/21/2026 8:24:32 PM +00:00
```

Lets verify the contents of our first Container vs Container 2

Container 1:
```powershell
PS C:\Users\cwilliams> Get-AzStorageBlob -Container "azcopylabcontainer" -Context $context

   AccountName: cyrilazcopystoracc, ContainerName: azcopylabcontainer

Name                 BlobType  Length          ContentType                    LastModified         AccessTier SnapshotTime                 IsDeleted  VersionId
----                 --------  ------          -----------                    ------------         ---------- ------------                 ---------  ---------
AzCopyLab/02 - Scar… BlockBlob 8207365         audio/mpeg                     2026-05-21 17:47:49Z Hot                                     False
AzCopyLab/Image (2)… BlockBlob 283341          image/png                      2026-05-21 17:26:59Z Hot                                     False
AzCopyLab/azure-a(1… BlockBlob 57644           image/png                      2026-05-21 17:53:20Z Hot                                     False
AzCopyLab/image (1)… BlockBlob 43314           image/png                      2026-05-21 17:26:59Z Hot                                     False
AzCopyLab/image (3)… BlockBlob 36796           image/jpeg                     2026-05-21 17:26:59Z Hot                                     False
```

Container 2:
```powershellPS C:\Users\cwilliams> Get-AzStorageBlob -Container "azcopylabcontainer2" -Context $context
PS C:\Users\cwilliams>
```
We can see it has nothing in it.

### Copy Using AzCopy

In Command Prompt, we'll run:
```
C:\>azcopy copy "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer/AzCopyLab/02 - Scary Monsters and Nice Sprites.mp3" "https://cyrilazcopystoracc.blob.core.windows.net/azcopylabcontainer2"
```
We get:

<img width="1478" height="813" alt="image" src="https://github.com/user-attachments/assets/2de99fe2-4082-4e0e-9498-f35b28a1179b" />

We can see one file was copied.

### Verify

Let's double check our transfer was succesful:

```powershell
PS C:\Users\cwilliams> Get-AzStorageBlob -Container "azcopylabcontainer2" -Context $context

   AccountName: cyrilazcopystoracc, ContainerName: azcopylabcontainer2

Name                 BlobType  Length          ContentType                    LastModified         AccessTier SnapshotTime                 IsDeleted  VersionId
----                 --------  ------          -----------                    ------------         ---------- ------------                 ---------  ---------
02 - Scary Monsters… BlockBlob 8207365         audio/mpeg                     2026-05-21 20:33:31Z Hot                                     False
```

Lets check the Portal:

<img width="1908" height="437" alt="image" src="https://github.com/user-attachments/assets/e3ddc446-8f5d-4de6-9365-fd393010666c" />


Nice!



