# Implement Network Traffic Management

In this lab, we'll configure Traffic Management using Azure Load Balancer and an Application Gateway.

## Set Up Environment

I'll create my initial environment using an ARM template.

We can see this template has 3 Virtual Machines, 3 Custom Script Exertions, 3 NICs, a Virtual Network & Network Security Group:

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/df211657-1ced-46b1-b0d7-e1c9ddd5bf1b" />

Our Parameters template will use the Standard_D2s_v3 VM SKU and an admin username of "localadmin"

<img width="1321" height="401" alt="image" src="https://github.com/user-attachments/assets/606b3295-fb0f-434f-bc62-aac7eebb3ce1" />

## Set Up an Azure Load Balancer

We'll use an Azure Load Balancer to distribute traffic across two of our VM's. 

Azure Load Balancer sits at Layer 4, the Transport Layer on the OSI model, 
and had its own IP address to accept connections, 
then it distributes those connections to specified machines.

We'll search and create a Load Balancer

<img width="91" height="91" alt="image" src="https://github.com/user-attachments/assets/499caea5-baff-4bfa-9f6f-744e98e471d0" />


We'll create a Standard, Public Load Balancer:


<img width="923" height="619" alt="image" src="https://github.com/user-attachments/assets/e9c745d6-d632-4fc2-bfb0-ac1bb3b5e559" />

Under 'Frontend IP configuration', we'll add a Frontend IP and create a new Public IP.

<img width="575" height="717" alt="image" src="https://github.com/user-attachments/assets/cbcae176-3646-48c0-91bf-180d0401e232" />

Under 'Backend pools', we'll configure a backend pool. 
This is the configuration to set what Virtual Machines traffic will be distributed to.

We'll set our VNet, NIC config, and VM's to be used:

<img width="1910" height="602" alt="image" src="https://github.com/user-attachments/assets/5bd8b0cf-f056-443c-a529-21b0ff1ebe72" />

Click 'Create'.

Lets go to our Load Balance, **Settings > Load balancing rules > Add**

We'll set up our Rule to configure the traffic that is distributed:

<img width="878" height="749" alt="image" src="https://github.com/user-attachments/assets/ec4eab5f-1b00-479d-97c7-b7cf20db17b3" />

Save.

Under the Frontend IP Configuration, we'll take note of the Public IP of the Load Balancer.

### Script Extension

If you remember earlier, our ARM Template included 3 Script Extensions:
```
"commandToExecute": "powershell.exe Install-WindowsFeature -name Web-Server -IncludeManagementTools && powershell.exe remove-item 'C:\\inetpub\\wwwroot\\iisstart.htm' && powershell.exe Add-Content -Path 'C:\\inetpub\\wwwroot\\iisstart.htm' -Value $('Hello World from ' + $env:computername) && powershell.exe New-Item -Path 'c:\\inetpub\\wwwroot' -Name 'image' -Itemtype 'Directory' && powershell.exe New-Item -Path 'c:\\inetpub\\wwwroot\\image\\' -Name 'iisstart.htm' -ItemType 'file' && powershell.exe Add-Content -Path 'C:\\inetpub\\wwwroot\\image\\iisstart.htm' -Value $('Image from: ' + $env:computername)"
```
If we take a closer look, we can see this part of the Script:
```
Add-Content -Path 'C:\\inetpub\\wwwroot\\iisstart.htm' -Value $('Hello World from ' + $env:computername)
```

Let's paste the Public IP of our Load Balancer into a new browser tab:


<img width="601" height="227" alt="image" src="https://github.com/user-attachments/assets/6719a262-3651-45a3-b3c8-15a4156b2b28" />

We can see our 'Hello World from (VM Name)" appears.

We can also see that the website is not secure, so it uses Port 80, 
like we specified earlier in our Load Balancer configuration.


## Azure Application Gateway

We'll setup an Application Gateway to balance Layer 7 traffic across our Azure VM's *(rather than Layer 4 traffic like the Load Balancer)*

First, we'll create a Subnet for our Application Gateway and Load Balancing Public IP to sit it.

We'll create that now:

<img width="825" height="435" alt="image" src="https://github.com/user-attachments/assets/3673a43d-897b-44e3-a283-d13d11617a06" />

Now we'll create an Application Gateway:

<img width="885" height="799" alt="image" src="https://github.com/user-attachments/assets/8ee1f68b-b23b-41ef-97d5-0f55fe9f5cf0" />

We'll go to 'Frontends' and create a new Public IP to forward traffic to:

<img width="767" height="211" alt="image" src="https://github.com/user-attachments/assets/c29dc911-32bf-4733-92ec-5a9f411c2f0e" />

Under 'Backends', we'll add a Backend and add our VMs and associated NICs:

<img width="573" height="403" alt="image" src="https://github.com/user-attachments/assets/3bddcaa8-0bc2-432b-a5dd-7a2eddeef7c6" />

We'll add two more Backend pools. One for /images and one for /videos.

<img width="762" height="423" alt="image" src="https://github.com/user-attachments/assets/f14cc8d1-f2ed-43db-a7c5-2f1923296842" />


Under 'Configuration', we'll add a Routing Table. 
This is where we will specify where traffic goes to based on the URL.

We'll set up our first Rule that listens on Port 80 under the Listener tab:

<img width="842" height="653" alt="image" src="https://github.com/user-attachments/assets/33ab1d2a-789f-46dc-9583-50dfbefb698b" />

Under the Backend tab, we'll create the Backend Pool that we want the traffic to go to:

<img width="831" height="690" alt="image" src="https://github.com/user-attachments/assets/ad48e8ae-04db-4f8d-8054-9e4a3e12000a" />

We'll create a new Backend setting:

<img width="843" height="561" alt="image" src="https://github.com/user-attachments/assets/676e85dd-144f-4aa8-ba1f-1882c0522545" />

Under Path-based routing, we'll configure a rule to route traffic to the right VM's based on the URL path:

Our first one will use the '/image' path

<img width="837" height="291" alt="image" src="https://github.com/user-attachments/assets/6419bcbe-deb4-4645-960e-6f55c9d46604" />

Our second path will use the '/video' path

<img width="845" height="301" alt="image" src="https://github.com/user-attachments/assets/5aab452e-c4e4-47cd-a5e5-1db080c5f6c2" />

We'll confirm our paths:

<img width="839" height="735" alt="image" src="https://github.com/user-attachments/assets/29459224-afe5-4744-99ff-3cb792e74d07" />

Review + Create.


### Verify

Now that our Application Gateway is deployed, we'll quickly go to our Application Gateway and go to **Monitoring > Backend health**

<img width="1328" height="731" alt="image" src="https://github.com/user-attachments/assets/185fa5b4-1eff-4da0-baa2-f7a6f19083e3" />


We can see everything is healthy.

Now let's use our Application Gateway:

If we take the Public IP that we created with our App Gateway and paste it into a browser with our configured paths, 
we get this:

```http://20.72.166.49/image/```

<img width="582" height="194" alt="image" src="https://github.com/user-attachments/assets/10223570-9196-4ea7-8b3f-19687b9eebcf" />

```http://20.72.166.49/video/```

<img width="664" height="263" alt="image" src="https://github.com/user-attachments/assets/b0fb5295-6ec6-4bc7-9ab5-5f5f0832585e" />

(No actual images or videos are currently configured but this would be the general idea in a real world scenario)

```http://20.72.166.49/``` gives us our 'Hello World' image again that we can see is coming form VM2.

<img width="675" height="206" alt="image" src="https://github.com/user-attachments/assets/3373aa5a-a473-4e7a-b2ae-82996eabacdc" />

