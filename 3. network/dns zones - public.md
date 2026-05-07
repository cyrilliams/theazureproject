# Set Up a Public DNS Zone

In this doc, we'll set up a DNS Zone, to automatically resolve our domain to our Azure Web Services

There are two types of DNS Zones: Public & Private

## Create DNS Zone

We'll search "DNS Zones"

<img width="516" height="72" alt="image" src="https://github.com/user-attachments/assets/356dba47-3ddc-4b17-99e9-b2aced848d1c" />

Then click 'Create'

<img width="859" height="711" alt="image" src="https://github.com/user-attachments/assets/46a110e3-b7dc-46d2-9d6e-1e20d7d25afa" />

We'll configure our DNS Zone and then click 'Create'

## Create DNS Record

Under the DNS Zone, we'll go to **DNS Management > Recordsets > Add**

We'll configure our Test DNS Record

<img width="571" height="572" alt="image" src="https://github.com/user-attachments/assets/1fb13bcf-085f-4837-934a-e8814d0503b3" />

We can see it's been added to our Recordset:

<img width="1646" height="581" alt="image" src="https://github.com/user-attachments/assets/1695a3b2-ceb2-4507-b3df-f6d193263f07" />

## Verify:

Now, if we run an nslookup using our newly created DNS record and Azure name server, it points to the IP address we set:

<img width="1113" height="626" alt="image" src="https://github.com/user-attachments/assets/ff974945-0ebc-4160-9554-9ff58a006417" />

*I was surprised at how fast the entry worked. Usually DNS entries take a couple minutes to work*

*We would use the IP address of a real server in the real world*
