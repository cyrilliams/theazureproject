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
