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


