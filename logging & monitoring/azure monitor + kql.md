# Azure Montior + KQL

In this doc, we'll go over Azure Monitor and KQL, the language used to query information from Azure Monitor.

## Create Resources
First, we'll need our Log Analytics Workspace

Log Analytics Workspaces collect data such as performance and usage logs and puts them into a central location.

We'll create our Lab Analytics Workspace:

<img width="773" height="673" alt="image" src="https://github.com/user-attachments/assets/556028ac-b599-4922-9496-43dbac734fbb" />

Next, we'll create a VM to monitor:

<img width="843" height="804" alt="image" src="https://github.com/user-attachments/assets/f603f528-904a-4b99-aa6b-53eaea620adf" />

### Enabled Monitoring on VM

We'll go to our VM, then **Monitoring > Insights/Monitor > Monitor Settings** *or Logs*

We'll configure our Monitor Settings by selecting our new Log Analytics Workstation:

<img width="946" height="342" alt="image" src="https://github.com/user-attachments/assets/9defcc95-06f8-4126-b329-f9ddfd09e587" />

Enable.

### Createa Data Collection Rule

Under the Log Analytics Workbook we created, we'll go to **Connect a data source > Azure virtal machines**

<img width="1905" height="729" alt="image" src="https://github.com/user-attachments/assets/d104bb08-9f8d-44d1-b06b-64386cb7cf5a" />

Name the Rule:

<img width="743" height="493" alt="image" src="https://github.com/user-attachments/assets/e263bba6-708e-4114-9d28-098bcd319dfb" />

Under Resources, we'll add our VM as a scope:

<img width="845" height="364" alt="image" src="https://github.com/user-attachments/assets/a4498036-c30d-4697-92af-4d5c0a42a279" />


Under Collect and deliver, we'll add a Data Source:

<img width="846" height="467" alt="image" src="https://github.com/user-attachments/assets/e30810e6-61d7-40eb-80d7-b1ed913fcc46" />

I'll enable two sources:

<img width="773" height="254" alt="image" src="https://github.com/user-attachments/assets/be11f5e8-6ddd-45e8-9196-bcaca2d7338b" />









### Connect and Generate Events

We'll RDP into our Machine:

<img width="407" height="245" alt="image" src="https://github.com/user-attachments/assets/21634eca-a183-4aa7-80b4-741fca72774d" />

We'll open up PowerShell and run: ```while ($true) { start-job {1..500000 | % {$_ * $_}} }``` which spikes the CPU and verify with Task Manager:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/102d82c0-c647-490c-85e6-d56172634d3e" />

I'll also do a couple of failed sign in attemps to show in the logs:

<img width="456" height="437" alt="image" src="https://github.com/user-attachments/assets/8ab8355d-f9f4-4643-9a72-432b64ac327f" />




## Azure Monitor Logs

Now we'll go to our **Log Analytics Workspace, Logs**, the click the purple Query button and KQL mode.

<img width="1910" height="811" alt="image" src="https://github.com/user-attachments/assets/da11bb0d-e895-4e4f-8fdb-e5a0f3c8b399" />


To show what Logs exist, we'll enter:
```kql
search *
| summarize count() by $table
```
<img width="986" height="384" alt="image" src="https://github.com/user-attachments/assets/f24499a3-a8c6-44bc-b806-ad57890f508b" />

Next, we'll check Heartbeat logs with:
```kql
Heartbeat
| take 10 
```
<img width="993" height="481" alt="image" src="https://github.com/user-attachments/assets/164780ad-d416-4a26-a549-fd2789e76efa" />

```take``` shows the specified number of rows

