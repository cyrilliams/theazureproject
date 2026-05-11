# Create a Virtual Machine Using an ARM Template

In this document, we will be deploying an Azure Virtual Machine using an ARM (Azure Resource Manager) Template.

This is useful in situtaitions where we want to provision mulitple instances of the same VM.
We can create/use an ARM template and deploy the VMs rather than sitting there and going throught the WEB GUI in-effeciently.

Let's take the stock Windows .json template from the Azure Virtual Machine Quickstart Template page:
*I've also uploaded the same .json template in this same folder*

We'll go to Custom Templates or 'Deploy  a custom template'

<img width="1531" height="716" alt="image" src="https://github.com/user-attachments/assets/a053955d-bac7-4bd5-b352-983a636587bf" />

We'll click 'Build your own template in the editor' and copy or load the .json template in:

<img width="1751" height="909" alt="image" src="https://github.com/user-attachments/assets/12bc2870-585e-438c-9ae6-a76d517c198f" />

### Parameters

We can see there are parameters that will need to be given a value based on user input:
There are some obvious ones like 'Name' and others like the size of the VM that will need to be specified.

<img width="1875" height="803" alt="image" src="https://github.com/user-attachments/assets/d46cd660-bbac-468c-9b27-affde8bdaf63" />



# Variables

Variables allow a value to be set and referrenced multiple times.
That was you are not re-entering 10.0.0.0/24 every time you need to specify the Subnet for example:

<img width="885" height="498" alt="image" src="https://github.com/user-attachments/assets/3244abd3-e262-498f-a913-d788f4b1706d" />


# Resources

When creating a VM, multiple resources will also need to be configured with it, especially if not set up already.
These include, a Public IP, Network Security Group, V-Net, etc

<img width="1358" height="915" alt="image" src="https://github.com/user-attachments/assets/ccb54a20-055e-4cf5-9c4d-61cb918edda6" />


Next we will go to Review + create and wait for validation to pass:

<img width="925" height="492" alt="image" src="https://github.com/user-attachments/assets/4422352f-c5e8-4b1e-81ab-ba7c7ff4814a" />

Then click create:

<img width="2540" height="857" alt="image" src="https://github.com/user-attachments/assets/0585cd30-2d63-4204-aa73-7d2ab0b48dc0" />


