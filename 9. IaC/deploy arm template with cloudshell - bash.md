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

