- Python includes a lightweight database called [SQLite](https://www.sqlite.org/) so you won’t need to set up a database just yet.

## Set up a database

This step is only necessary if you’d like to work with a “large” database engine like PostgreSQL, MariaDB, MySQL, or Oracle. To install such a database, consult the [database installation information](https://docs.djangoproject.com/en/5.1/topics/install/#database-installation).

---

## Install the Django code

Installation instructions are slightly different depending on whether you’re installing a distribution-specific package, downloading the latest official release, or fetching the latest development version.

### **Installing an official release with `pip`**

This is the recommended way to install Django.

1. Install [pip](https://pip.pypa.io/). The easiest is to use the [standalone pip installer](https://pip.pypa.io/en/latest/installation/). If your distribution already has **`pip`** installed, you might need to update it if it’s outdated. If it’s outdated, you’ll know because installation won’t work.
2. Take a look at [venv](https://docs.python.org/3/tutorial/venv.html). This tool provides isolated Python environments, which are more practical than installing packages systemwide. It also allows installing packages without administrator privileges. The [contributing tutorial](https://docs.djangoproject.com/en/5.1/intro/contributing/) walks through how to create a virtual environment.
3. After you’ve created and activated a virtual environment, enter the command:
    
    ```powershell
    py -m pip install Django
    ```
    
4. Verify installation using the command:
    
    ```powershell
    py -m django --version
    ```
    

---

## Creating a project

If this is your first time using Django, you’ll have to take care of some initial setup. Namely, you’ll need to auto-generate some code that establishes a Django [project](https://docs.djangoproject.com/en/5.1/glossary/#term-project) – a collection of settings for an instance of Django, including database configuration, Django-specific options and application-specific settings.

From the command line, **`cd`** into a directory where you’d like to store your code, then run the following command:

```powershell
django-admin startproject mysite
```

<aside>
💡 You’ll need to avoid naming projects after built-in Python or Django components. In particular, this means you should avoid using names like **`django`** (which will conflict with Django itself) or **`test`** (which conflicts with a built-in Python package).

</aside>

---

## Folder Structure

```powershell
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

These files are:

- The outer **`mysite/`** root directory is a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
- **`manage.py`**: A command-line utility that lets you interact with this Django project in various ways. You can read all the details about **`manage.py`** in [django-admin and manage.py](https://docs.djangoproject.com/en/5.1/ref/django-admin/).
- The inner **`mysite/`** directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. **`mysite.urls`**).
- **`mysite/__init__.py`**: An empty file that tells Python that this directory should be considered a Python package. If you’re a Python beginner, read [more about packages](https://docs.python.org/3/tutorial/modules.html#tut-packages) in the official Python docs.
- **`mysite/settings.py`**: Settings/configuration for this Django project. [Django settings](https://docs.djangoproject.com/en/5.1/topics/settings/) will tell you all about how settings work.
- **`mysite/urls.py`**: The URL declarations for this Django project; a “table of contents” of your Django-powered site. You can read more about URLs in [URL dispatcher](https://docs.djangoproject.com/en/5.1/topics/http/urls/).
- **`mysite/asgi.py`**: An entry-point for ASGI-compatible web servers to serve your project. See [How to deploy with ASGI](https://docs.djangoproject.com/en/5.1/howto/deployment/asgi/) for more details.
- **`mysite/wsgi.py`**: An entry-point for WSGI-compatible web servers to serve your project. See [How to deploy with WSGI](https://docs.djangoproject.com/en/5.1/howto/deployment/wsgi/) for more details.

---

## Dev Server

```powershell
py manage.py runserver
```

You’ll see the following output on the command line:

```bash
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

August 13, 2024 - 15:50:53
Django version 5.1, using settings 'mysite.settings'
Starting development server athttp://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

Now that the server’s running, visit http://127.0.0.1:8000/ with your web browser. You’ll see a “Congratulations!” page, with a rocket taking off. It worked! 🚀🚀🚀

---

(To serve the site on a different port, see the [**`runserver`**](https://docs.djangoproject.com/en/5.1/ref/django-admin/#django-admin-runserver) reference.)

**Automatic reloading of [`runserver`](https://docs.djangoproject.com/en/5.1/ref/django-admin/#django-admin-runserver)**

<aside>
💡 The development server automatically reloads Python code for each request as needed. You don’t need to restart the server for code changes to take effect. However, some actions like adding files don’t trigger a restart, so you’ll have to restart the server in these cases.

</aside>