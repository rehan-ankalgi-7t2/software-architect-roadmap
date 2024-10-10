By default, the [**`DATABASES`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-DATABASES) configuration uses **SQLite**. If you’re new to databases, or you’re just interested in trying Django, this is the easiest choice. SQLite is included in Python, so you won’t need to install anything else to support your database. When starting your first real project, however, you may want to use a more scalable database like PostgreSQL, to avoid database-switching headaches down the road.

If you wish to use another database, see [details to customize and get your database running](https://docs.djangoproject.com/en/5.1/topics/install/#database-installation).

While you’re editing **`mysite/settings.py`**, set [**`TIME_ZONE`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-TIME_ZONE) to your time zone.

---

While you’re editing **`mysite/settings.py`**, set [**`TIME_ZONE`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-TIME_ZONE) to your time zone.

Also, note the [**`INSTALLED_APPS`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-INSTALLED_APPS) setting at the top of the file. That holds the names of all Django applications that are activated in this Django instance. Apps can be used in multiple projects, and you can package and distribute them for use by others in their projects.

By default, [**`INSTALLED_APPS`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-INSTALLED_APPS) contains the following apps, all of which come with Django:

- [**`django.contrib.admin`**](https://docs.djangoproject.com/en/5.1/ref/contrib/admin/#module-django.contrib.admin) – The admin site. You’ll use it shortly.
- [**`django.contrib.auth`**](https://docs.djangoproject.com/en/5.1/topics/auth/#module-django.contrib.auth) – An authentication system.
- [**`django.contrib.contenttypes`**](https://docs.djangoproject.com/en/5.1/ref/contrib/contenttypes/#module-django.contrib.contenttypes) – A framework for content types.
- [**`django.contrib.sessions`**](https://docs.djangoproject.com/en/5.1/topics/http/sessions/#module-django.contrib.sessions) – A session framework.
- [**`django.contrib.messages`**](https://docs.djangoproject.com/en/5.1/ref/contrib/messages/#module-django.contrib.messages) – A messaging framework.
- [**`django.contrib.staticfiles`**](https://docs.djangoproject.com/en/5.1/ref/contrib/staticfiles/#module-django.contrib.staticfiles) – A framework for managing static files.

These applications are included by default as a convenience for the common case

---

Some of these applications make use of at least one database table, though, so we need to create the tables in the database before we can use them. To do that, run the following command:

```python
python manage.py migrate
```

The [**`migrate`**](https://docs.djangoproject.com/en/5.1/ref/django-admin/#django-admin-migrate) command looks at the [**`INSTALLED_APPS`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-INSTALLED_APPS) setting and creates any necessary database tables according to the database settings in your **`mysite/settings.py`** file and the database migrations shipped with the app (we’ll cover those later). 

You’ll see a message for each migration it applies. If you’re interested, run the command-line client for your database and type **`\dt`** (PostgreSQL), **`SHOW TABLES;`** (MariaDB, MySQL), **`.tables`** (SQLite), or **`SELECT TABLE_NAME FROM USER_TABLES;`** (Oracle) to display the tables Django created.