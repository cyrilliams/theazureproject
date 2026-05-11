# Tags

<img width="100" height="100" alt="image" src="https://github.com/user-attachments/assets/2cf4bbf1-f661-46ae-9423-f11f4c17d07a" />

In this doc, we'll add Azure Tags to our Resources.

## Tagging an Already Created Resource

I already have a resource I'd like to Tag. Let's apply that here.

We'll click the Resource; in my case, I'll use my 'applicationsandweb-rg' Resource Group, then click 'Tags'

<img width="1322" height="463" alt="image" src="https://github.com/user-attachments/assets/54dae225-7946-49cb-8a1a-68a5e0a9e2d9" />

Next, we'll enter our Tag name and Value. Then click Apply.

<img width="1311" height="116" alt="image" src="https://github.com/user-attachments/assets/d12edf21-7093-4cf5-91b8-644cc612fd21" />

I like to think of the Tag as a Category and the value as the options.

We can see our Tag has been created:

<img width="1316" height="103" alt="image" src="https://github.com/user-attachments/assets/ab67b656-26e6-469f-95d4-9b68ff7a28e7" />


## Multiple Values

I'll create a different Tag (Location : New York) for a different Resource, to see how using a different Value works.

<img width="1053" height="268" alt="image" src="https://github.com/user-attachments/assets/157a8229-4e42-4c35-a214-2d565037e108" />

If we go to or search 'Tags', we can see we have our created Tags here:

<img width="1639" height="335" alt="image" src="https://github.com/user-attachments/assets/3b6493c6-e275-498b-8f29-dabb31c779b1" />

Notice that they appear as seperate Tags, even though they are both tagged under 'Location'

## Multiple Resources in a Tag

Tagging can be useful to logically group multiple Resources accross different regions and Resource Groups.

Here we can see that I've added two different Resource Groups with seperate locations to our Location : Florida Tag (which I know doesn't make perfect sense for our example)

<img width="1329" height="336" alt="image" src="https://github.com/user-attachments/assets/39a6d933-239d-4cd3-8072-53d2af80e1e7" />


