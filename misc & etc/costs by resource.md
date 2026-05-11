# Finding Costs By Resource 
##### *And Saving Money*
Let's take an even granular view of our cost analysis.

We'll start by selecting our current Subscription as the current Cost Management scope:

<img width="554" height="73" alt="image" src="https://github.com/user-attachments/assets/98079a69-4c3a-4663-9370-3b2169581067" />

I was astonished to see that I've used $7 worth of resources for this month, and it's only the first day. 
I was even more surprised to see that my forecasted monthly cost would be over $60... *oops*

<img width="1571" height="1004" alt="image" src="https://github.com/user-attachments/assets/bf9c5bd3-eec2-4933-bc64-2f56e425c933" />

Let's see why. We'll click view details in 'Cost by resource'

We can see that Storage is taking up the most (and only) amount of funds:

<img width="2549" height="1144" alt="image" src="https://github.com/user-attachments/assets/75cd5af3-d1cd-47ef-a07b-03b5dc378fe3" />

I want to see what service specifically in that group was charging us so much already.
I'll click 'Cost by resource' and click 'Resource':

<img width="187" height="282" alt="image" src="https://github.com/user-attachments/assets/556a4022-c84d-46b3-b053-6cf8600de0d7" />

Here, we can see that it given us a more detailed reason of what is charging us.

It looks like SFTP is enabled for Blob Storage Account.

*This must be an error on my end because I am not using Blob storage, only Azure File storage*

<img width="2218" height="951" alt="image" src="https://github.com/user-attachments/assets/af0875c5-e7ca-47c6-bfcf-0f88d8ba1b12" />

Let's go to that storage account and find the SFTP option under 'Settings':

<img width="1816" height="1105" alt="image" src="https://github.com/user-attachments/assets/3eab2f8c-8e9e-48fe-bd2b-1b70874860ae" />

This is not something I am actively using, and may have enabled during the Storage Account's creation.
*This feature charges per hour when turned on*

<img width="1476" height="323" alt="image" src="https://github.com/user-attachments/assets/01aa4979-c740-4517-9160-ebb772660728" />

And that's how we save money.

It's a great idea to check your billing section every once in a while!
