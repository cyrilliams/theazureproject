# Adding Entra ID Roles

Let's create a user who only has access to read in Entra ID.

### User Creation

In Entra, let's create a new user:

<img width="701" height="580" alt="image" src="https://github.com/user-attachments/assets/aaf84db3-d9ac-433a-b3d8-ba8ca9c2ecb6" />

We'll assign whatever properties we want to our new user.

Under assignments, we'll add a group and add some roles:

<img width="685" height="182" alt="image" src="https://github.com/user-attachments/assets/965faca0-7902-451c-8569-681c2081fdc9" />

For now, I'll add him to the a Help Desk User Group and add a Global Reader role.


<img width="524" height="237" alt="image" src="https://github.com/user-attachments/assets/6aaab495-e1da-4124-aa48-94e4439382bb" />

Now, let's look at our user in the User section

<img width="1624" height="724" alt="image" src="https://github.com/user-attachments/assets/18aa93b6-0266-49c6-94f2-2121a6f95f15" />

Let's login and verify that our roles and permissions are set correctly:

<img width="350" height="293" alt="image" src="https://github.com/user-attachments/assets/f7119bbd-5882-47ba-98b3-505c1476f4b2" />

If I try to create a new user, due to the reader role, the 'Create new user' button is greyed out:

<img width="317" height="215" alt="image" src="https://github.com/user-attachments/assets/5867744a-1923-45d4-826f-024fdcbdf3fc" />

---

It's important to note that these roles only affect what a user can do in Entra, not in Azure. 
Let's configure that in the next doc.
