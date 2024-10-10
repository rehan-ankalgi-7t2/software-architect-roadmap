Django messages framework provides a way to temporarily store messages in one request and retrieve them for display in a subsequent request. It’s typically used to provide feedback to users, such as notifications of success, warnings, errors, or information after a form submission or other user actions.

### Key Concepts of Django Messages

1. **Message Levels**: Django messages are categorized into different levels of severity:
    - **DEBUG**: Intended for debugging purposes, typically not shown to users.
    - **INFO**: General information, usually to inform the user of some action.
    - **SUCCESS**: Indicates that an action was successful.
    - **WARNING**: Alerts the user to some condition that might require attention.
    - **ERROR**: Indicates that something went wrong.
2. **Storage Backends**: Django provides different backends for storing messages. The most commonly used one is the `SessionStorage`, which stores messages in the user's session.
3. **Middleware**: To use the messages framework, you need to have `MessageMiddleware` and `SessionMiddleware` enabled in your Django project.
4. **Message Tags**: These allow you to customize the CSS classes or tags that correspond to different message levels.

### Setting Up Django Messages

### 1. **Ensure Middleware is Enabled**

In your `settings.py`:

```python
MIDDLEWARE = [
    ...
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    ...
]

INSTALLED_APPS = [
    ...
    'django.contrib.messages',
    ...
]

```

### 2. **Using Messages in Views**

To add a message in a view, you use the `messages` module. Django provides several shortcut functions to add messages corresponding to different levels:

```python
from django.contrib import messages

def my_view(request):
    # Add a success message
    messages.success(request, 'Your profile was updated successfully.')

    # Add an error message
    messages.error(request, 'Something went wrong.')

    # Redirect or render a template
    return redirect('some_view_name')

```

### Available Methods:

- `messages.debug(request, "Your debug message")`
- `messages.info(request, "Your info message")`
- `messages.success(request, "Your success message")`
- `messages.warning(request, "Your warning message")`
- `messages.error(request, "Your error message")`

### 3. **Displaying Messages in Templates**

To display messages in your templates, you can iterate over the `messages` context variable:

```html
{% if messages %}
    <ul class="messages">
        {% for message in messages %}
            <li class="{{ message.tags }}">{{ message }}</li>
        {% endfor %}
    </ul>
{% endif %}

```

In this example, `{{ message.tags }}` will render the message's level as a CSS class (like `success`, `error`, etc.), which you can style accordingly.

### 4. **Customizing Message Tags**

You can customize the CSS classes associated with each message level by defining a custom mapping in `settings.py`:

```python
from django.contrib.messages import constants as message_constants

MESSAGE_TAGS = {
    message_constants.DEBUG: 'debug',
    message_constants.INFO: 'info',
    message_constants.SUCCESS: 'success',
    message_constants.WARNING: 'warning',
    message_constants.ERROR: 'error',
}

```

### 5. **Message Storage Backends**

Django supports different storage backends for messages:

- **`SessionStorage`** (default): Stores messages in the session.
- **`CookieStorage`**: Stores messages in cookies, useful if you want to avoid using sessions.

You can change the message storage backend in `settings.py`:

```python
MESSAGE_STORAGE = 'django.contrib.messages.storage.session.SessionStorage'
# or
MESSAGE_STORAGE = 'django.contrib.messages.storage.cookie.CookieStorage'

```

### 6. **Message Context Processor**

Django automatically adds messages to the context of templates when the `MessageMiddleware` is enabled. However, if you need more control, you can add the context processor manually:

```python
TEMPLATES = [
    {
        ...
        'OPTIONS': {
            'context_processors': [
                ...
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

```

### Advanced Usage

### 1. **Message Tags Customization**

You might want to use different HTML tags or CSS classes for different message levels:

```python
{% for message in messages %}
    <div class="alert alert-{{ message.tags }}">
        {{ message }}
    </div>
{% endfor %}

```

### 2. **Adding Extra Tags**

You can add extra tags to messages:

```python
messages.success(request, 'Profile updated successfully.', extra_tags='profile-update')

```

In the template:

```html
<div class="alert {{ message.tags }}"> <!-- Will include 'profile-update' and 'success' -->
    {{ message }}
</div>

```

### 3. **Manually Handling Message Storage**

If you need to manually access the messages (e.g., in a custom middleware or context processor):

```python
from django.contrib.messages import get_messages

def my_custom_view(request):
    storage = get_messages(request)
    for message in storage:
        print(message)

```

### Conclusion

The Django messages framework is a powerful tool for providing feedback to users. It's simple to use, flexible, and integrates well with Django's template system. By customizing the message tags and storage options, you can adapt it to fit the needs of your application.