# Creating the Azure V-Net

Next, I want to create an Azure V-Net to create resources that will need to be on a network, like a VM.
I'll also test this once I get my on prem environment setup to connect the physical LAN to the virtual LAN.
Lucky for me, creating a V-Net is FREE!

## Creation

I created the V-Net using my subscription.
I also had to create a resource group to put the V-Net in.
I picked EAST US because that is a popular region and it is closest to me.
I have it an easy name to follow as well.

<img width="1001" height="874" alt="image" src="https://github.com/user-attachments/assets/3cf1bca8-38f3-41d1-b890-859c2a02b633" />

## Subnets

For the subnet, I just used a /24 address. 
I probably could have went higher since I won't have much on each subnet.
I do plan to segregate my resources by subnet.
My main V-Net will be 10.0.0.X and maybe other resources will follow 10.0.1.X and 10.0.2.X

<img width="963" height="691" alt="image" src="https://github.com/user-attachments/assets/f9b5bf39-22a3-42dc-ae98-d8b09ae3d5f6" />

## Deploy

Time to create!

<img width="1881" height="476" alt="image" src="https://github.com/user-attachments/assets/da8573d4-3a60-467d-bfc6-095343955c39" />

Luckily this only took a couple seconds:

<img width="702" height="77" alt="image" src="https://github.com/user-attachments/assets/afbd737d-793f-4239-b2d7-abda6fb0f8bb" />


## Private or Public?

For now, I will keep everything internal. 
I do not need to create a public IP yet since I don't have any resources that need to talk to the internet.

