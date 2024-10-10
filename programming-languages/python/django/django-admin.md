Generating admin sites for your staff or clients to add, change, and delete content is tedious work that doesn’t require much creativity. For that reason, Django entirely automates creation of admin interfaces for models.

Django was written in a newsroom environment, with a very clear separation between “content publishers” and the “public” site. Site managers use the system to add news stories, events, sports scores, etc., and that content is displayed on the public site. 

<aside>
💡 Django solves the problem of creating a unified interface for site administrators to edit content.

</aside>

The admin isn’t intended to be used by site visitors. It’s for site managers.

---

# **Creating an admin user**

First we’ll need to create a user who can login to the admin site. Run the following command:

```python
python manage.py createsuperuser
```

Enter your desired username and press enter.

```python
Username: admin
```

You will then be prompted for your desired email address:

```python
Email address: admin@example.com
```

The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.

```python
Password: **********
Password (again): *********
Superuser created successfully.
```

The Django admin site is activated by default.

Now, open a web browser and go to “/admin/” on your local domain – e.g., http://127.0.0.1:8000/admin/. You should see the admin’s login screen:

!https://docs.djangoproject.com/en/5.1/_images/admin01.png