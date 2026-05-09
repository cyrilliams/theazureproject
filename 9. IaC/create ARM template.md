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


