## **Django Models: A Deep Dive**

### **Understanding the Core**

Django models are the foundation for defining the structure of your application's data. Essentially, they map to database tables, but they offer a Pythonic interface for interacting with that data.

**Key Components:**

- **Model Class:** A Python class that subclasses `django.db.models.Model`.
- **Fields:** Attributes within the model class, representing database columns. Each field has a specific data type and potential constraints.
- **Managers:** Objects that provide an interface for querying and manipulating model instances. The default manager is `objects`.
- **Metaclass:** An optional class within a model that defines additional meta-information, such as database table name, ordering, permissions, etc.

### **Model Fields**

Django offers a rich set of field types to accommodate various data needs:

- **CharField**: For storing text with a maximum length.
- **TextField**: For storing larger amounts of text without a length limit.
- **IntegerField**: For storing integer values.
- **DecimalField**: For storing decimal numbers with precision and scale.
- **DateField**: For storing dates.
- **DateTimeField**: For storing dates and times.
- **BooleanField**: For storing boolean values (True or False).
- **ForeignKey**: For creating one-to-many relationships.
- **OneToOneField**: For creating one-to-one relationships.
- **ManyToManyField**: For creating many-to-many relationships.

**Example:**

**Python**

```bash
from django.db import models

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.CharField(max_length=50)   
    publication_date = models.DateField()
    price = models.DecimalField(max_digits=10,    decimal_places=2)
```

### **Model Managers**

The default manager, `objects`, provides methods for querying and manipulating model instances. You can create custom managers to provide additional functionality.

**Python**

```bash
from django.db import models

class BookManager(models.Manager):
    def published_recently(self):
        return self.filter(publication_date__gte=timezone.now() - datetime.timedelta(days=7))

class Book(models.Model):
    # ... other fields
    objects = BookManager()
```

### **Model Relationships**

Django supports three types of relationships:

- **One-to-One:** A single instance of one model is related to a single instance of another model.
- **One-to-Many:** One instance of a model can be related to multiple instances of another model.
- **Many-to-Many:** Instances of one model can be related to multiple instances of another model, and vice versa.

**Example:**

**Python**

```python
class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    title = models.CharField(max_length=100)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
```

### **Model Metaclass**

The `Meta` class within a model allows you to define additional options:

**Python**

```python
class Book(models.Model):
    # ... fields

    class Meta:
        ordering = ['-publication_date']
        verbose_name = 'Book'
        verbose_name_plural = 'Books'
```

### **Additional Considerations**

- **Model Validation:** Django provides mechanisms for validating data before saving it to the database.
- **Model Inheritance:** You can create abstract base classes and model hierarchies.
- **Database Schema Creation:** Django automatically generates the database schema based on your models.
- **QuerySets:** Django's ORM provides powerful querysets for filtering, ordering, and aggregating data.

By understanding these core concepts and leveraging Django's rich feature set, you can effectively model your application's data and build robust, scalable web applications.

**Would you like to explore any specific aspect of Django models in more detail, such as querysets, model validation, or relationships?**

---

# Creating Models

<aside>
💡 **Philosophy**

A model is the single, definitive source of information about your data. It contains the essential fields and behaviors of the data you’re storing. Django follows the [DRY Principle](https://docs.djangoproject.com/en/5.1/misc/design-philosophies/#dry). The goal is to define your data model in one place and automatically derive things from it.

This includes the migrations - unlike in Ruby On Rails, for example, migrations are entirely derived from your models file, and are essentially a history that Django can roll through to update your database schema to match your current models.

</aside>

In our poll app, we’ll create two models: **`Question`** and **`Choice`**. A **`Question`** has a question and a publication date. A **`Choice`** has two fields: the text of the choice and a vote tally. Each **`Choice`** is associated with a **`Question`**.

These concepts are represented by Python classes. Edit the **`polls/models.py`** file so it looks like this:

```python
# polls_app/models.py
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")

class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

---

# Activating Models

That small bit of model code gives Django a lot of information. With it, Django is able to:

- Create a database schema (**`CREATE TABLE`** statements) for this app.
- Create a Python database-access API for accessing **`Question`** and **`Choice`** objects.

But first we need to tell our project that the **`polls`** app is installed.

<aside>
💡 Django apps are “pluggable”: You can use an app in multiple projects, and you can distribute apps, because they don’t have to be tied to a given Django installation.

</aside>

To include the app in our project, we need to add a reference to its configuration class in the [**`INSTALLED_APPS`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-INSTALLED_APPS) setting. The **`PollsConfig`** class is in the **`polls/apps.py`** file, so its dotted path is **`'polls.apps.PollsConfig'`**. Edit the **`mysite/settings.py`** file and add that dotted path to the [**`INSTALLED_APPS`**](https://docs.djangoproject.com/en/5.1/ref/settings/#std-setting-INSTALLED_APPS) setting. It’ll look like this:

```python
# mysite/settings.py
INSTALLED_APPS = [
    "polls.apps.PollsConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

Now Django knows to include the **`polls`** app. Let’s run another command:

```python
python manage.py makemigrations polls
```

By running **`makemigrations`**, you’re telling Django that you’ve made some changes to your models (in this case, you’ve made new ones) and that you’d like the changes to be stored as a *migration*.

Migrations are how Django stores changes to your models (and thus your database schema) - they’re files on disk. You can read the migration for your new model if you like; it’s the file **`polls/migrations/0001_initial.py`**. Don’t worry, you’re not expected to read them every time Django makes one, but they’re designed to be human-editable in case you want to manually tweak how Django changes things