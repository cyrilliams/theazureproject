# Setting Up Identity & Management

First, I'll setup my first user (myself) as a Global Admin in Entra,
that way I have permissions to do everything I need to in Azure.

I'll go to my user account:

<img width="2088" height="532" alt="image" src="https://github.com/user-attachments/assets/ee4ae837-e617-4a47-9b1e-8cd2edbb0c06" />

Next, go to Assigned Roles and add the Global Admin assignment:

<img width="2200" height="685" alt="image" src="https://github.com/user-attachments/assets/3da06aa7-0bb0-45db-bff1-36febf5cebbb" />

Just to get better understanding of how different roles work and operate,
I'll create separate accounts with assigned roles:

<img width="1318" height="250" alt="image" src="https://github.com/user-attachments/assets/99febeae-7c43-4ded-adc6-7d025de406cb" />

Although these are all fully Entra based, I will eventually setup a Virtual Machine, running Windows Server,
and use Active Directory and create user's through there, to best simulate a hybrid environment.



## Security & MFA for Admins

We will enable Security Defaults, which pushes mandatory MFA for all admins. 
This is a must for any and all environments.

<img width="2198" height="1182" alt="image" src="https://github.com/user-attachments/assets/1925676b-e75e-47d1-be21-ef0020a7c8db" />

I also think it is particular useful to ensure Microsoft Authenticator is enabled for all users.
This is something we push in my current environment and I see why it works.

<img width="2196" height="778" alt="image" src="https://github.com/user-attachments/assets/48c503e2-44d6-4e83-8a72-76d76e97f18e" />


# Conditional Access and PIM

### Conditional Access

While I will not be setting up Conditional Access and PIM (Privileged Identity Management) due to lack of licensing, there are things I would want to set up in a real world environment.
Currently, we use CA to say, "Hey, if you are not signing in from at least in the United States, you definitely cannot login"
If I was all enrolling devices with Intune (which we hopefully will soon in this lab), I would probably also want to enforce access to certain resources can only be accessed from compliant devices.



### PIM

I don't believe we have PIM setup in my current environment but it can and will come in handy to harden the environment and reduce risk.
This would go hand and hand with enforcing MFA for privileged roles like Global Admins. 
If we wanted to set it up, we could require re-authentication for functions that require Admin Roles.

## Exclusion Group

Lastly, I'll set up an exclusion group which will be the main admin account. 
This will be just in case I lock myself out or mess something up with my Entra based admin account.

<img width="952" height="651" alt="image" src="https://github.com/user-attachments/assets/3ce26d49-7a1b-496f-a9c6-07248817e272" />




