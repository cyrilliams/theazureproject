# Implement Virtual Networks

In this lab, we will go over creating two virtual networks (V-Nets) and establishing communication between them.

## Create VNet (Portal):

First, I'll create a VNet using the Portal:

<img width="781" height="722" alt="image" src="https://github.com/user-attachments/assets/bfc89b18-d990-44ab-966f-1143d051a801" />

Our network will use the 10.20.0.0/16 address range:

<img width="534" height="102" alt="image" src="https://github.com/user-attachments/assets/5ae11c21-5478-448b-b81d-411c54613d3d" />


I'll configure the Subnets we need:

The first one will use a 10..20.10.0/24 address range:

<img width="1110" height="439" alt="image" src="https://github.com/user-attachments/assets/5425ff14-7543-42b3-afd6-81bc7834ed2b" />

The second will use a 10.20.20.0/24 address range:

<img width="1107" height="434" alt="image" src="https://github.com/user-attachments/assets/4c7526db-d92f-4880-8c8a-957bb033fee9" />

Run validation and create:

<img width="736" height="791" alt="image" src="https://github.com/user-attachments/assets/57a1c883-e01a-4b73-aefd-9ec1d9e3f4f3" />

After verifying this, we'll create another using a template:

In our VNet, we'll go to **Automation > Export template > ARM template > Download (Template & Parameters)**

<img width="1633" height="735" alt="image" src="https://github.com/user-attachments/assets/02f19f69-afa6-45b7-99e4-d75637281fd4" />

## Create VNets with a Template:

To be as effecient as possible, we'll redeploy the VNet using a template. 

First, we'll make some changes to the ARM Templates.

### Edit ARM Templates

I'll open up the JSON with VSCode:

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/5a169974-600a-4531-afa9-cfe91860cd46" />

I'll change every instance of CoreServicesVNet to ManufacturingVnet,
change SharedServicesSubnet to SensorSubnet1,
DatabaseSubnet to SensorSubnet2,
and change the addresses to use a 10.30.0.0/16 address.

<img width="1427" height="911" alt="image" src="https://github.com/user-attachments/assets/fcaeea36-db80-4f7a-88e0-5954f3312902" />

For the Parameters file, we'll change CoreServicesVnet to ManufacturingVnet

Before:

<img width="971" height="291" alt="image" src="https://github.com/user-attachments/assets/c0169927-2ff1-469c-a28b-f1b58486be7b" />

After:

<img width="1062" height="261" alt="image" src="https://github.com/user-attachments/assets/cab2b8af-137c-4736-a5ea-8a7e9492c132" />

### Deploy Custom Templates

We'll deploy a template using the 'Deploy a custom template' tab:

<img width="218" height="36" alt="image" src="https://github.com/user-attachments/assets/de4b7ce1-39be-4e9e-a572-633f396060ac" />

We'll do **Build your own > Edit template > Load file > Upload Template.json > Save**

Then **Edit parameters > Load file > Upload Template.json > Save**

Azure recongnizes our VNet Name:

<img width="476" height="147" alt="image" src="https://github.com/user-attachments/assets/527a295a-c95d-43f0-832a-0ebf4c900b1a" />

Review and Create!

Looks like our VNet & two subnets were created! Lets verify them:

<img width="1321" height="354" alt="image" src="https://github.com/user-attachments/assets/ec64137d-90cf-4aa0-9634-14df592ba6d1" />

VNet is correct:

<img width="1898" height="383" alt="image" src="https://github.com/user-attachments/assets/dd31774e-22a4-453a-ae2b-0121db68cc38" />

### Fixing Mistakes

Looks like I missed something because the DatabaseSubnet is active. Let's go back and review:

<img width="647" height="333" alt="image" src="https://github.com/user-attachments/assets/d9ca5c2f-0cec-4014-9c20-f8e31cb75ab4" />

Found it:

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/115cd997-1f77-4728-9cac-084bfe3f09d9" />

I'll replace it with the correct name:

<img width="1920" height="1032" alt="image" src="https://github.com/user-attachments/assets/f6db2063-33a2-43f8-af6c-c695132ac9b5" />

I'll delete the VNet and redeploy using the updated Template:

Now it's correct:

<img width="1900" height="508" alt="image" src="https://github.com/user-attachments/assets/4c3c4f57-5c9b-46ad-9b58-d93947e2d2ca" />


## Create Application Security Group and Network Security Group

We'll quicily create an ASG:

<img width="851" height="437" alt="image" src="https://github.com/user-attachments/assets/e8541d0f-fbe7-49e9-8006-8a2c27e98000" />


We'll create an NSG as well:

<img width="898" height="459" alt="image" src="https://github.com/user-attachments/assets/36ae268d-eec8-4bd0-b9d7-3cbab3492c8b" />

To associate the NSG with a Subnet, 
we'll go to **NSG > Settings > Subnets > Associate**

<img width="565" height="204" alt="image" src="https://github.com/user-attachments/assets/61c3c996-a7e6-4a93-8744-5f4dabacee1d" />

Save.

### Inbound ASG Allow Rule

We will not create an inbound rule to allow traffic from the ASG to that subnet.

We'll go to **Settings > Inbound security rules > Add**

Configure the Inbound rule to allow internet traffic from the ASG:

<img width="560" height="794" alt="image" src="https://github.com/user-attachments/assets/8bd5b41d-cfeb-4194-b125-e0ff9d370e47" />

*The priority is 100 to tell the NSG that this rule is the highest priority*

### Outbound Internet Deny Rule

We'll go to **Settings > Outbound security rules > Add**

<img width="567" height="753" alt="image" src="https://github.com/user-attachments/assets/dd9bbae5-5147-461d-858f-4c22653398a7" />

*The priority is set to 4096 to tell the NSG that this is the lowest priority*

## Configure Public DNS Zone

We'll configure a Public DNS Zone to resolve our domain name.

We'll create our Zone:

<img width="860" height="667" alt="image" src="https://github.com/user-attachments/assets/9e51aba8-a80e-4b28-b8b2-2c2fdb1ed413" />

Under that DNS Zone, we'll go to **DNS Management > Recordsets > Add**

<img width="573" height="869" alt="image" src="https://github.com/user-attachments/assets/6e6dadae-31c2-48e7-9824-763f4dda1751" />


Now we'll verify it using nslookup and one of Azure's name servers:

We can see it resolved to the IP address I've set:

<img width="1113" height="626" alt="image" src="https://github.com/user-attachments/assets/6ecffd4e-a833-42fe-98aa-126a98962f3d" />

Let's change the IP just to be sure. I'll change it to 10.40.1.1:

<img width="570" height="786" alt="image" src="https://github.com/user-attachments/assets/bcdec56d-f435-4963-b9d6-a3566d6521b8" />

Boom:

<img width="1113" height="626" alt="image" src="https://github.com/user-attachments/assets/82e772f0-9840-4c6f-a928-9d5d5269fdc9" />

## Create a Private DNS Zone:

We'll create a Private DNS Zone to resolve names to services in our VNet's:

<img width="842" height="663" alt="image" src="https://github.com/user-attachments/assets/9f216fb0-8207-4061-8c9a-f177df1ae056" />

Under that DNS Zone, we'll go to **DNS Management > Virtual network links > Add**

Name and Link it to our ManufacturingVnet

<img width="787" height="636" alt="image" src="https://github.com/user-attachments/assets/429f7c6a-cc70-4a95-9f25-320524a150f4" />

We'll go to **DNS Management > Recordsets > Add**, and add what would be our VM's to they could resolve.

In this scenario, the IP of 10.30.1.4 would resolve to sensorvm.privatevnet.cyriltest.site
<img width="569" height="523" alt="image" src="https://github.com/user-attachments/assets/7ccb8bf6-d345-460d-955f-3395734dfde3" />


## Test with VM

I'll create a VM real quick and verify the IP address:

<img width="775" height="578" alt="image" src="https://github.com/user-attachments/assets/1a546e99-f7ed-47d6-a7d2-3d95a61cad3a" />

