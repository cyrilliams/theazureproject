# Setting Up a Metric Alert

Alerts are extremely useful to have setup.

If a server or VM goes down or exceeds a set percentage of usage, we want to know.

Let's create an alert rule:

<img width="1906" height="651" alt="image" src="https://github.com/user-attachments/assets/ea2b46a7-0409-4051-8b31-f41d384dc5a7" />

Let's select a scope. I'll choose some Resource Groups that I would like the alerts to focus on:

<img width="837" height="617" alt="image" src="https://github.com/user-attachments/assets/50d3332d-93be-41d8-b730-4e630dd9432b" />

Under 'Condition', I'll choose 'Resource Health' under 'see all signals'

I'll also choose a couple conditions such as if the Container is updated or unavailable:

<img width="796" height="419" alt="image" src="https://github.com/user-attachments/assets/52f9711b-4a70-425c-9662-69e9d1e1a408" />

#### Create Action Group

Next, I'll create an action group to choose how I will get notified and alerted.

<img width="988" height="522" alt="image" src="https://github.com/user-attachments/assets/72ecb3cc-50eb-4fdc-b6f7-e66cf0f053c8" />

I'll setup SMS and Push notifications to my Azure App on my phone. I could also setup email and a voice call too!

<img width="971" height="247" alt="image" src="https://github.com/user-attachments/assets/f8dc3688-6380-4924-8e0c-ff419166697f" />

*I'll skip the Actions & Tags*

Now it'll take us back to the alert rule creation.

<img width="954" height="230" alt="image" src="https://github.com/user-attachments/assets/a72fffd1-f89e-4103-b149-6d7158475219" />

Next, we will give the alert rule a name and description if we would like:

<img width="961" height="477" alt="image" src="https://github.com/user-attachments/assets/06297143-c325-4edc-98a1-c0817ca46a3d" />

We can now view it in our Alert Rules:

<img width="1905" height="496" alt="image" src="https://github.com/user-attachments/assets/349e96bb-48a2-4304-b36f-107f436f2b29" />

*This particular alert doesn't do anything but we could be notified if we wanted for various things in Azure*
