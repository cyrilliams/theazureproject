# Implement Monitoring

In this lab, we'll create an alert, send it to an action group to be notified about specified events. 
We'll trigger the alerts and check our activity logs.

## Create Environment from ARM Template

We'll create an Resource Group that includes a Windows Server VM, NIC, Public IP, Vnet & Subnet and Network Security Group

<img width="1292" height="865" alt="image" src="https://github.com/user-attachments/assets/3aa29504-a88b-4b07-9193-fbab0f10d9f1" />

This is what's included:

<img width="1911" height="692" alt="image" src="https://github.com/user-attachments/assets/ab87aac0-18f8-49a3-ad92-28acefb0003c" />

We'll go to Azure Monitor:

<img width="68" height="91" alt="image" src="https://github.com/user-attachments/assets/d57200ba-71df-442a-8d9f-39e1bf662dc8" />

**Monitor > Insights > Virtual Machines > Configure insights > Enable**

<img width="1635" height="475" alt="image" src="https://github.com/user-attachments/assets/f16775b6-2a16-4da6-94d7-ef2d4778625b" />

**Review + enable**

<img width="1125" height="415" alt="image" src="https://github.com/user-attachments/assets/a43e2498-b5e8-4856-be30-6f78039a88b1" />


## Create an Alert

In Azure Montitor, we'll go to **Monitor > Alerts > Create > Alert rule**

We'll choose the scope or our Alerts. 
You can do the whole Subscription, Resource Group or Resource:

<img width="825" height="733" alt="image" src="https://github.com/user-attachments/assets/3355bd68-82a4-4953-a29d-3cd0247f9961" />

Under the 'Condition' tab, we'll click 'See all signals', and find 'Delete Virtual Machine'

<img width="839" height="351" alt="image" src="https://github.com/user-attachments/assets/128a88ff-12dc-4ddb-8ab5-4e088c01f3de" />

We'll keep the default settings:

<img width="1005" height="260" alt="image" src="https://github.com/user-attachments/assets/440de0a3-d598-461f-9a94-844c6d6dc2e2" />

### Configure Action Group

On the next tab, we'll create an Action Group.

<img width="970" height="524" alt="image" src="https://github.com/user-attachments/assets/c83eaf31-5162-4fe6-9010-ad8052393b6a" />

For Notifications, we'll set it to your preferred notification methods:

<img width="567" height="703" alt="image" src="https://github.com/user-attachments/assets/867356c2-b593-4167-969b-8c0ae48ad739" />

Name the Notification type:

<img width="974" height="213" alt="image" src="https://github.com/user-attachments/assets/bd5f1480-82ab-4e55-8927-f8212c5f9e18" />

Create the Action Group.

<img width="1098" height="300" alt="image" src="https://github.com/user-attachments/assets/b2635378-9a75-4336-9c78-883216d7b0c8" />

Now back in the Rules configuration, we'll name the Rule and Create:

<img width="1005" height="491" alt="image" src="https://github.com/user-attachments/assets/e455d584-7880-4f94-8e27-3a5a01f4473f" />

## Test and Verify Alert

Let's see if our Alert is set up correctly. 
Since our Alert is set to trigger once we delete a VM, 
lets delete a VM.

We'll trigger the Delete for our VM:

<img width="842" height="566" alt="image" src="https://github.com/user-attachments/assets/17f0ed97-6570-489f-b18c-29084ce1cd47" />

And now we wait...

#### Email:

We get this email:

<img width="1590" height="704" alt="image" src="https://github.com/user-attachments/assets/39ea4d77-47de-491b-bdba-d4071d3a764e" />


#### Text Message:

We recieved this text message:

<img width="828" height="1792" alt="image" src="https://github.com/user-attachments/assets/6f5def8e-2f9c-44e2-bf0a-812caa3efa88" />

#### Azure iOS App Notification:

And an Azure iOS App Notification:

<img width="297" height="177" alt="image" src="https://github.com/user-attachments/assets/15b06ad3-b15c-47d5-bd76-c713b64a1323" />

Amazing!

## Create Alert Processing Rule

Let's create an Alert Processing Rule to silence notifications at a certain time.

Under **Monitor > Alerts > Create > Alert processing rule**, choose our scope:

<img width="1020" height="208" alt="image" src="https://github.com/user-attachments/assets/f7371bcc-ba88-4506-8fca-7a730acfc697" />

For this example, we'll choose the 'Suppress notification' Rule type:

<img width="1020" height="170" alt="image" src="https://github.com/user-attachments/assets/b013269e-c6a6-41dd-9a7d-1b825099cecf" />

Under 'Scheduling', choose our time frame. 
You can do a specific time or recurring time frame:


<img width="977" height="404" alt="image" src="https://github.com/user-attachments/assets/66c1e09d-7d19-4e38-83d1-f4f2e430a1ad" />


Name the Rule and Create:

<img width="1018" height="471" alt="image" src="https://github.com/user-attachments/assets/85b87050-128e-4528-81ed-19dcc4bcdf9f" />


## Use Azure Log Queries

We'll go to **Azure Monitor > Logs**, choose the scope. Then go to Queries (purple icon), Virtual machines > Count heartbeats > Run:

<img width="882" height="653" alt="image" src="https://github.com/user-attachments/assets/b0a8b350-7324-4d3c-9aff-ab9a9a40f50c" />

We get this Result:

<img width="291" height="162" alt="image" src="https://github.com/user-attachments/assets/883573a9-2888-426d-9d9a-5bd6b980208e" />

### Run Custom KQL Query

We'll swap over to KQL mode and enter this Query:

```
 InsightsMetrics
 | where TimeGenerated > ago(1h)
 | where Name == "UtilizationPercentage"
 | summarize avg(Val) by bin(TimeGenerated, 5m), Computer //split up by computer
 | render timechart
```

Click Run and we will get this chart:

<img width="1299" height="750" alt="image" src="https://github.com/user-attachments/assets/bc917277-326b-4217-a7ad-63907f132e87" />

*This KQL Query shows us the time and Utilization Percentage in 5 minute increments by computer*


