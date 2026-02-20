**The following project guide is NOT mine. This was created by [Luke J Bryne](https://www.lukejbyrne.com/). I'll link his page [here](https://www.lukejbyrne.com/az104-projects)**





---


<img width="256" height="256" alt="image" src="https://github.com/user-attachments/assets/4f951e4f-0845-44fa-bc88-a2e5f78635df" />


# AZ104 Projects x5

## **Project 1: Azure Compute and Identity Management**

**Topics Covered**: VMs, RBAC, Azure AD, Policies, Encryption, Cost Management

**Time**: ~0.75 hours


This project covers deploying a secure storage account, creating VNets and NSGs for isolation, enabling encryption, and automating resource deployment using ARM templates. It demonstrates networking and storage fundamentals.

### **Scenario**

A company wants to deploy a secure storage account, ensure network isolation for its resources, enforce data encryption, and use templates to automate the deployment of resources.

### **Steps**

1. **Create a Virtual Network (VNet)**
    - Go to **Azure Portal** > **Virtual Networks** > **Create**.
    - Add two subnets: **"Web"** and **"Database"**.
        - + Subnet > Name “Database” > IPv4 > 10.0.0.0 > /27 Size > Enable private subnet > Enable Service Endpoints for Microsoft.Storage for secure access.
        - + Add a Subnet > Name “Web” > IPv4 > 10.0.1.0 > /27 Size.
        - Review and create.
    - Azure automatically sets up **intra-VNet communication**.
    - Subnets within the same VNet can communicate directly by default.
2. **Deploy a Network Security Group (NSG)**
    - Navigate to **Network Security Groups** > **Create**.
    - Associate it with the **"Web"** subnet.
    - Go to Resource > Subnets > Associate > Web
    - Add inbound rules:
        - Allow HTTPS (443) traffic from the internet.
            - Now go to Inbound security rules > Add > Destination port 443 / Service HTTPS > Add
        - Block all other inbound internet traffic (except Azure services if needed).
            - Add > Destination port * > Add
            - If you need to allow any specific ports like SSH / RDP then just add them as an increased priority
            - Note that you can’t modify the default ones but you can override them with a higher priority; AllowVnetInBound, AllowAzureLoadBalancerInBound, DenyAllInBound
3. **Create and Configure a Storage Account**
    - Navigate to **Storage Accounts** > **Create**.
    - Configure:
        - **Replication**: Choose locally redundant storage (LRS) or geo-redundant storage (GRS).
        - **Private Endpoint**: Ensure secure access from the database subnet.
            - Go to Advanced > Permitted scope… From storage accounts that have a private endpoint… > Next
            - Disable public access > Add private endpoint > Select database subnet
        - **Encryption**: Use Microsoft-managed keys.
4. **Deploy the VNet and Storage Account Using ARM Templates**
    - For both Vnet and Storage Account go to Automation > Export Template > Download
    - Navigate to **Templates specs** > Import template > select template file (template.json from the download > Create.
    - Then click three dots of your new template in Template specs > Deploy
5. **Test Access and Encryption**
    - Generate a **Shared Access Signature (SAS)** token to test secure access.
        - Go to Storage accounts > your storage account > Security + networking > Shared access signature > Select all Allowed resource types > Generate SAS
        - **Test Blob Service SAS URL**
            - Use **Azure Storage Explorer**:
                - Download and install [Azure Storage Explorer](https://azure.microsoft.com/en-us/products/storage/storage-explorer/).
                - Go to **"Connect to Azure Resources"** > **Use a shared access signature (SAS) URI**.
                - Paste the **Connection String**
                - Test if you can upload/download files (e.g. create a blob container and upload).
            - Use **AzCopy**:
                - Install AzCopy: [Download AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).
                - Run a test upload/download:
                    
                    ```bash
                    bash
                    Copy code
                    azcopy copy "file-to-upload.txt" "https://proj2saqwerty.blob.core.windows.net/container-name/file-to-upload.txt?[SAS]"
                    ```
                    
                - Replace `[SAS]` with the SAS token.

---
## **Project 2: Azure Networking and Storage**

**Topics Covered**: Virtual Networks, NSGs, Storage Accounts, Encryption, Protocols, ARM Templates

**Time**: ~0.75 hours

### **Summary**

This project covers deploying a secure storage account, creating VNets and NSGs for isolation, enabling encryption, and automating resource deployment using ARM templates. It demonstrates networking and storage fundamentals.

### **Scenario**

A company wants to deploy a secure storage account, ensure network isolation for its resources, enforce data encryption, and use templates to automate the deployment of resources.

### **Steps**

1. **Create a Virtual Network (VNet)**
    - Go to **Azure Portal** > **Virtual Networks** > **Create**.
    - Add two subnets: **"Web"** and **"Database"**.
        - + Subnet > Name “Database” > IPv4 > 10.0.0.0 > /27 Size > Enable private subnet > Enable Service Endpoints for Microsoft.Storage for secure access.
        - + Add a Subnet > Name “Web” > IPv4 > 10.0.1.0 > /27 Size.
        - Review and create.
    - Azure automatically sets up **intra-VNet communication**.
    - Subnets within the same VNet can communicate directly by default.
2. **Deploy a Network Security Group (NSG)**
    - Navigate to **Network Security Groups** > **Create**.
    - Associate it with the **"Web"** subnet.
    - Go to Resource > Subnets > Associate > Web
    - Add inbound rules:
        - Allow HTTPS (443) traffic from the internet.
            - Now go to Inbound security rules > Add > Destination port 443 / Service HTTPS > Add
        - Block all other inbound internet traffic (except Azure services if needed).
            - Add > Destination port * > Add
            - If you need to allow any specific ports like SSH / RDP then just add them as an increased priority
            - Note that you can’t modify the default ones but you can override them with a higher priority; AllowVnetInBound, AllowAzureLoadBalancerInBound, DenyAllInBound
3. **Create and Configure a Storage Account**
    - Navigate to **Storage Accounts** > **Create**.
    - Configure:
        - **Replication**: Choose locally redundant storage (LRS) or geo-redundant storage (GRS).
        - **Private Endpoint**: Ensure secure access from the database subnet.
            - Go to Advanced > Permitted scope… From storage accounts that have a private endpoint… > Next
            - Disable public access > Add private endpoint > Select database subnet
        - **Encryption**: Use Microsoft-managed keys.
4. **Deploy the VNet and Storage Account Using ARM Templates**
    - For both Vnet and Storage Account go to Automation > Export Template > Download
    - Navigate to **Templates specs** > Import template > select template file (template.json from the download > Create.
    - Then click three dots of your new template in Template specs > Deploy
5. **Test Access and Encryption**
    - Generate a **Shared Access Signature (SAS)** token to test secure access.
        - Go to Storage accounts > your storage account > Security + networking > Shared access signature > Select all Allowed resource types > Generate SAS
        - **Test Blob Service SAS URL**
            - Use **Azure Storage Explorer**:
                - Download and install [Azure Storage Explorer](https://azure.microsoft.com/en-us/products/storage/storage-explorer/).
                - Go to **"Connect to Azure Resources"** > **Use a shared access signature (SAS) URI**.
                - Paste the **Connection String**
                - Test if you can upload/download files (e.g. create a blob container and upload).
            - Use **AzCopy**:
                - Install AzCopy: [Download AzCopy](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).
                - Run a test upload/download:
                    
                    ```bash
                    bash
                    Copy code
                    azcopy copy "file-to-upload.txt" "https://proj2saqwerty.blob.core.windows.net/container-name/file-to-upload.txt?[SAS]"
                    ```
                    
                - Replace `[SAS]` with the SAS token.

---

## **Project 3: Monitoring, Backup, and Recovery**

**Topics Covered**: Azure Monitor, Alerts, Backup, Encryption, Protocols, Log Queries

**Time**: ~0.5 hours

This project demonstrates integrating applications with Entra ID, managing users and groups, setting up conditional access policies, enabling MFA, and monitoring authentication activity.

### **Summary**

This project focuses on setting up Azure Monitor for performance monitoring, enabling backups for data recovery, configuring disaster recovery with Site Recovery, and analyzing logs with Log Analytics.

### **Scenario**

A company wants to monitor their infrastructure for performance issues, ensure data recovery in case of failure, enforce secure data transfer, and analyze logs for insights.

Note: Use the VM from Project 1

### **Steps**

1. **Configure Azure Monitor for VMs**
    - Go to the VM > Monitoring > **Insights** > Azure **Monitor > Enable VM Insights > Enable > Enable > Configure**.
    - Go to the VM > Monitoring > Alerts > View + set up > Switch on high CPU > Save
        - Threshold: 80%.
        - Action Group: Email or other notification methods.
2. **Set Up Azure Ba22**
    - Navigate to **Recovery Services Vault** > **Create**.
    - Configure a **Backup Policy**:
        - Daily backups with custom retention (e.g., 7 days).
        - Enable encryption for data at rest.
    - Perform a manual backup and verify its status.
3. **Implement Azure Site Recovery**
    - Go to the VM > **Disaster Recovery** > Enable replication to a secondary region.
    - Configure replication policies and test the failover process.
    - Monitor replication health using **Azure Monitor**.
4. **Query Logs in Azure Monitor**
    - Navigate to **Log Analytics Workspace** > **Logs**.
    - Write and execute queries to analyze metrics:
        
        ```
        Perf
        | where ObjectName == "Processor" and CounterName == "% Processor Time"
        | summarize Avg_CPU = avg(CounterValue) by bin(TimeGenerated, 5m)
        
        ```
        
    - Visualize results as charts for insights.
5. **Secure Backup and Recovery**
    - Ensure the **Recovery Services Vault** uses encryption:
        - Check properties for encryption configuration.
    - Verify TLS encryption for all backup-related communication.

---

## **Project 4: Entra ID Integration and Identity Management**

**Topics Covered**: Entra ID, User and Group Management, App Registration, Conditional Access, MFA

**Time**: ~0.75 hours

### **Summary**

This project demonstrates integrating applications with Entra ID, managing users and groups, setting up conditional access policies, enabling MFA, and monitoring authentication activity.

### **Scenario**

A company wants to integrate their web application with Entra ID for authentication, manage user and group permissions, enforce conditional access policies, and enable multi-factor authentication (MFA) for added security.

### **Steps**

1. **Create Users and Groups in Entra ID**
    - Navigate to **Entra ID** > **Users** > **Create User**.
    - Create a few users with different roles (e.g., Admin, Developer, Reader).
    - Go to **Groups** > **Create Group** > Add the newly created users.
2. **Register an Application in Entra ID**
    - Navigate to **App Registrations** > **New Registration**.
    - Enter a name, supported account types, and redirect URI (e.g., for a web application).
    - **API Permissions**: Add permissions for **Microsoft Graph** (e.g., User.Read).
    - **Certificates & Secrets**: Create a client secret for the application.
3. **Assign Users and Groups to the Application**
    - Go to **Enterprise Applications** > Select the newly registered app.
    - Navigate to **Users and Groups** > **Add User/Group** > Assign the previously created groups to the application.
4. **Configure Conditional Access**
    - Navigate to **Entra ID** > **Security** > **Conditional Access** > **New Policy**.
    - Create a policy to require MFA for all users accessing the application.
    - Set conditions, such as location-based access or device compliance.
    - Enable the policy and test by logging in with different users.
5. **Enable Multi-Factor Authentication (MFA)**
    - Go to **Entra ID** > **Users** > **Multi-Factor Authentication**.
    - Enable MFA for selected users.
    - Test the login process to ensure MFA is required.
6. **Monitor Sign-In Activity**
    - Navigate to **Entra ID** > **Sign-ins**.
    - Review sign-in logs to verify successful and failed authentication attempts.

---

## **Project 5: Azure App Service Deployment and Scaling**

**Topics Covered**: App Service, Deployment Slots, Autoscaling, Backup, Monitoring

**Time**: ~0.75 hours

### **Summary**

This project focuses on deploying a web application using Azure App Service, utilizing deployment slots for testing, configuring autoscaling based on metrics, and setting up backups.

### **Scenario**

A company wants to deploy a web application using Azure App Service, set up deployment slots for testing, enable autoscaling based on demand, and configure backups for disaster recovery.

### **Steps**

1. **Create an App Service**
    - Navigate to **App Services** > **Create**.
    - Select the subscription, resource group, and enter a name for the app.
    - Choose a **Runtime Stack** (e.g., .NET, Node.js, Python) and select a pricing tier.
    - Review and create the App Service.
2. **Deploy the Web Application**
    - Use **Azure DevOps** or **GitHub Actions** to set up a CI/CD pipeline.
    - Deploy the sample web application to the App Service.
    - Verify the deployment by accessing the application URL.
3. **Set Up Deployment Slots**
    - Navigate to the **App Service** > **Deployment Slots** > **Add Slot**.
    - Create a slot named **"Staging"**.
    - Deploy a new version of the application to the **Staging** slot.
    - **Swap** slots to promote the staging version to production after testing.
4. **Configure Autoscaling**
    - Navigate to the **App Service Plan** > **Scale Out (App Service Plan)**.
    - Set up **autoscaling** based on metrics such as CPU usage or request count.
    - Define rules (e.g., scale out by 1 instance if CPU > 70% for 10 minutes).
5. **Backup and Restore**
    - Navigate to the **App Service** > **Backups** > **Configure**.
    - Set up a backup schedule to back up the app and its associated database.
    - Perform a manual backup and verify it by restoring to a new App Service.
6. **Monitor and Configure Alerts**
    - Navigate to **App Service** > **Monitoring** > **Metrics**.
    - Set up metrics to monitor app performance (e.g., CPU usage, response time).
    - Configure **Alerts** to notify when metrics exceed defined thresholds.
