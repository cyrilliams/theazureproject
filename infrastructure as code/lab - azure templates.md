# Manage Azure Resources By Using ARM Templates

In this doc, we'll go over 5 different ways to create Resources using Templates in Azure:



# Create an Azure Resource Manager Template

In this doc, we'll first create an ARM template, that we will deploy via multiple methods after.

In this lab, we'll be deploying an Azure Disk, then redeploying using an ARM template.

## Create ARM Template in Azure Portal

In Azure Portal, we'll first search or find 'Disks', then 'Create'

<img width="642" height="206" alt="image" src="https://github.com/user-attachments/assets/37225d3e-450c-4b7d-9148-ebb160352dce" />

We'll name the disk and select the size of the disk.

<img width="1068" height="832" alt="image" src="https://github.com/user-attachments/assets/00d6397e-fc9e-4bd4-bf09-9eeb8771ec1a" />

We'll skip the rest of the configuration settings and create the disk.

<img width="572" height="180" alt="image" src="https://github.com/user-attachments/assets/6308c768-2aea-4f1d-a671-739537e71e12" />

With the Disk selected, we'll go to **Automation > Export Template**

We'll click Download to download the Template:

<img width="1612" height="1038" alt="image" src="https://github.com/user-attachments/assets/922aa62c-b8f1-443e-ab74-f452d361fa86" />

We can take note of the Resource settings, including the SKU, location, size and network settings:

<img width="1240" height="708" alt="image" src="https://github.com/user-attachments/assets/40adac51-9130-4ed6-904f-03a7f85c4566" />

We'll also download the Parameters Template file as well:

<img width="1612" height="818" alt="image" src="https://github.com/user-attachments/assets/feb22163-c763-49b3-8280-8b8d28bc5335" />

Now we have our Template and Parameter JSON files:

<img width="550" height="156" alt="image" src="https://github.com/user-attachments/assets/7d1b7635-41df-4bc4-bfa5-085674389ef3" />

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


# Deploy the Arm Template Using Cloud Shell

In this doc, we'll create another Disk via our ARM template, using Azure Cloud Shell.

## Launch Cloud Shell and Edit JSON

In the Azure Portal, we'll launch our Cloud Shell.

<img width="43" height="43" alt="image" src="https://github.com/user-attachments/assets/8a14a24b-c396-430a-ad52-3fec27565420" />

Switch or make sure you are in PowerShell.


<img width="1340" height="452" alt="image" src="https://github.com/user-attachments/assets/72c86d57-525b-4015-ab88-c5d73b60dfe7" />

Under 'Manage files', we'll select upload

<img width="224" height="134" alt="image" src="https://github.com/user-attachments/assets/88af851c-d9d7-431b-b42a-f5e7b57d0c15" />

We'll upload both the Template and Parameters JSON files:

<img width="470" height="255" alt="image" src="https://github.com/user-attachments/assets/ae332010-c790-4ec7-b0a5-8aedb82bea53" />

It also tells us exactly where they're placed, in '/home/cyril'



We'll click the 'Editor' button at the top, then select our 'template.json' file:

<img width="1888" height="1024" alt="image" src="https://github.com/user-attachments/assets/01c22043-689d-42cf-b2bc-4eb0f8c24688" />


We'll change the Parameter from 'disks_az104_disk1_name' to 'disk_name' in two locations,
and change the default value of the parameter to 'az104-disk3'

<img width="1084" height="568" alt="image" src="https://github.com/user-attachments/assets/4b5e112d-b33d-4072-b2f6-1f389d482711" />

We'll do **Ctrl+S** to save the JSON file


Next, we'll edit the Parameters JSON file by changing 'disks_az104_disk1_name' to 'disk_name'


<img width="1056" height="362" alt="image" src="https://github.com/user-attachments/assets/4534d6f0-5752-4e34-bd31-1f64153c3cd0" />


We'll do **Ctrl+S** to save the JSON file


## Deploy Template

We'll run:
```
New-AzResourceGroupDeployment -ResourceGroupName armtemplate-rg -TemplateFile template.json -TemplateParameterFile parameters.json
```

We can see it has successfully ran and created our Resource:

<img width="1727" height="454" alt="image" src="https://github.com/user-attachments/assets/0e71a487-dc2d-4e42-97bc-4a329f73942c" />


Now in Azure Portal, we can see a successfully created 3rd Disk:

<img width="2547" height="776" alt="image" src="https://github.com/user-attachments/assets/52899ebf-1c5f-4cb3-8fef-dce393a93826" />


# Deploy an ARM Template Using Cloud Shell - Bash

In this doc, we'll use Bash running in Azure's Cloud Shell to create a resource using an ARM template:



## Edit the JSON File

Open Azure's Cloud Shell and confirm you're using Bash, not PowerShell.

Run 'ls' to see directories and files. 

I've already uploaded my Templates from before, but if you have not, upload them using 'Manage files > Upload'

<img width="1276" height="382" alt="image" src="https://github.com/user-attachments/assets/6e1def5a-5e2a-4b1f-869a-901e43a29d88" />

I'll use the Editor, select my Template.JSON and edit the default value of the Parameter to 'az104-disk4'

<img width="1515" height="550" alt="image" src="https://github.com/user-attachments/assets/057e6afd-a66f-4ffe-9ef6-50711d7f559e" />

I'll save with **CTRL+S**

## Deploy the Template

In the Bash Cloud Shell, we'll deploy the Template with ```az deployment group create```

The fill script will be:
```
cyril [ ~ ]$ az deployment group create --resource-group armtemplate-rg --template-file template.json --parameters parameters.json
```

We'll get this back after waiting a couple seconds:

<img width="1655" height="1090" alt="image" src="https://github.com/user-attachments/assets/98c18800-7cad-4b31-9442-296c3c482c73" />

Now if we go back to Azure Portal, we can see our 4th Azure Disk:

<img width="2552" height="776" alt="image" src="https://github.com/user-attachments/assets/5b191afd-c335-4568-87bc-bc5723b1b5e7" />


# Deploy a Resource with Azure Bicep

In this doc, we'll create our final Disk using an Azure Bicep file.

## Use Bicep File

We'll first upload our Azure Bicep file into our Cloud Shell - Bash session.

<img width="476" height="134" alt="image" src="https://github.com/user-attachments/assets/1744a10a-c055-4b32-9d94-2b80ee2f2660" />

We'll open the Editor and select our Bicep file.

Next we'll change a couple of lines:

Change the managedDiskName value, line 2, to az104-disk5.

Change the diskSizeinGiB value; line 7, to 32. 

Change the sku name value, line 26, to Premium_LRS. `

<img width="1108" height="859" alt="image" src="https://github.com/user-attachments/assets/16aa442f-413d-4901-ab90-928b20dec3b5" />

We'll save with **Ctrl+S**

In the Bash Cloud Shell, we'll run:
```
cyril [ ~ ]$ az deployment group create --resource-group armtemplate-rg --template-file azuredeploydisk.bicep
```

We can verify it was created using:
```
cyril [ ~ ]$ az disk list --resource-group armtemplate-rg --output table
```
Which gives us:
```
cyril [ ~ ]$ az disk list --resource-group armtemplate-rg --output table
Name         ResourceGroup    Location    Zones    Sku          SizeGb    ProvisioningState
-----------  ---------------  ----------  -------  -----------  --------  -------------------
az104-disk1  armtemplate-rg   eastus      1        Premium_LRS  32        Succeeded
az104-disk2  armtemplate-rg   eastus      1        Premium_LRS  32        Succeeded
az104-disk3  armtemplate-rg   eastus      1        Premium_LRS  32        Succeeded
az104-disk4  armtemplate-rg   eastus      1        Premium_LRS  32        Succeeded
az104-disk5  armtemplate-rg   eastus               Premium_LRS  32        Succeeded
```

<img width="952" height="216" alt="image" src="https://github.com/user-attachments/assets/c855c28a-934e-41ec-be0a-84c91fab29b8" />


We can also verify this in Azure Portal:

<img width="2548" height="743" alt="image" src="https://github.com/user-attachments/assets/ae8bc7d0-3c33-4ef8-ad0a-a99e7bf67590" />



## Delete Resource Group

To not get charged, we'll delete our Resource Group using the Cloud Shell.

With PowerShell, we'll use:
```
Remove-AzResourceGroup -Name armtemplate-rg
```
With Bash, we'll use:
```
az group delete --name armtemplate-rg
```

Now, if you try to access the Resource Group, it cannot be found:

<img width="1246" height="968" alt="image" src="https://github.com/user-attachments/assets/0afbc683-8ac2-4518-8cfc-1ac71d5f4591" />




