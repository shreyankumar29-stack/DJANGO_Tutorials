# Part 03 - Commands Reference 🛠️

This file contains the commands, URLs, and important configuration used during **Part 03 - Templates** of the Corey Schafer Django Tutorial Series.

---

# 🚀 Start the Development Server

From the directory containing `manage.py`:

```bash
python manage.py runserver
```

Starts Django's development server.

The default server URL is:

```text
http://127.0.0.1:8000/
```

---

# 🔌 Run Server on a Different Port

```bash
python manage.py runserver 8001
```

Runs the development server on port `8001`.

URL:

```text
http://127.0.0.1:8001/
```

---

# 🛑 Stop the Development Server

```text
CTRL + C
```

Stops the running Django development server.

---

# 🐍 Check Django Version

```bash
python -m django --version
```

Displays the currently installed Django version.

---

# 🌐 Important URLs

## Home Page

```text
http://127.0.0.1:8000/
```

Loads the blog home page.

---

## About Page

```text
http://127.0.0.1:8000/about/
```

Loads the blog About page.

---

## Static CSS File

```text
http://127.0.0.1:8000/static/blog/main.css
```

Useful for checking whether Django can find and serve the CSS file.

---

# 📁 Important Project Commands

## Create Django App

If the app has not already been created:

```bash
python manage.py startapp blog
```

Creates the `blog` Django application.

---

# 📦 Install Django

If Django is not installed in the active virtual environment:

```bash
pip install django
```

---

# 🔍 Check Installed Django Package

```bash
pip show django
```

Displays information about the installed Django package.

---

# 🎨 Static Files Configuration

These are configuration/code snippets rather than terminal commands.

---

## Load Static Template Tags

At the top of `base.html`:

```django
{% load static %}
```

This enables Django's static file template tags.

---

## Link CSS File

```html
<link rel="stylesheet" href="{% static 'blog/main.css' %}">
```

Django resolves the static file path automatically.

---

# 📂 Static File Structure

The CSS file must be located at:

```text
blog/
└── static/
    └── blog/
        └── main.css
```

The template refers to it as:

```django
{% static 'blog/main.css' %}
```

---

# 🧩 Template Commands / Tags

## Extend Base Template

```django
{% extends "blog/base.html" %}
```

Allows a child template to inherit the structure of `base.html`.

---

## Create a Content Block

```django
{% block content %}
{% endblock content %}
```

Defines a section that child templates can replace.

---

## Display a Variable

```django
{{ variable }}
```

Example:

```django
{{ post.title }}
```

---

## Loop Through Posts

```django
{% for post in posts %}
    {{ post.title }}
{% endfor %}
```

Loops through the `posts` collection.

---

# 🔗 URL Configuration

## Include App URLs

Inside the project `urls.py`:

```python
path('', include('blog.urls')),
```

This connects the root URL to the Blog application's URL configuration.

---

## Blog Home URL

Inside `blog/urls.py`:

```python
path('', views.home, name='blog-home'),
```

Maps `/` to the `home` view.

---

## Blog About URL

```python
path('about/', views.about, name='blog-about'),
```

Maps `/about/` to the `about` view.

---

# 🖥️ Rendering a Template

Inside `views.py`:

```python
return render(request, 'blog/home.html')
```

Renders the `home.html` template.

---

# 📤 Passing Context to a Template

```python
context = {
    'posts': posts
}

return render(request, 'blog/home.html', context)
```

Passes the `posts` data from the View to the Template.

---

# 🧪 Static File Debugging

If this URL:

```text
http://127.0.0.1:8000/static/blog/main.css
```

returns a `404` error, check:

```text
1. blog/static/blog/main.css exists
2. {% load static %} is present
3. {% static 'blog/main.css' %} is correct
4. django.contrib.staticfiles is in INSTALLED_APPS
5. STATIC_URL is configured
6. blog.apps.BlogConfig is installed
```

---

# ⚙️ Important Settings

## Static Files App

`settings.py` should contain:

```python
'django.contrib.staticfiles',
```

inside:

```python
INSTALLED_APPS
```

---

## Static URL

```python
STATIC_URL = '/static/'
```

---

## Blog App

The Blog app should be registered:

```python
'blog.apps.BlogConfig',
```

---

# 📌 Quick Command Reference

| Command | Purpose |
|---|---|
| `python manage.py runserver` | Start development server |
| `python manage.py runserver 8001` | Start server on port 8001 |
| `python -m django --version` | Check Django version |
| `python manage.py startapp blog` | Create Blog app |
| `pip install django` | Install Django |
| `pip show django` | Show Django package information |
| `CTRL + C` | Stop development server |

---

# 📌 Quick Template Reference

| Syntax | Purpose |
|---|---|
| `{{ variable }}` | Display a variable |
| `{% for %}` | Loop through data |
| `{% extends %}` | Inherit a template |
| `{% block %}` | Define/override a template block |
| `{% load static %}` | Load static template tags |
| `{% static %}` | Generate static file URL |

---

# 🎯 Part 03 Command Checklist

- [x] Start Django development server
- [x] Check Django version
- [x] Test Home URL
- [x] Test About URL
- [x] Test Static CSS URL
- [x] Use `render()`
- [x] Pass context to templates
- [x] Use `{% extends %}`
- [x] Use `{% block %}`
- [x] Use `{% for %}`
- [x] Load static files
- [x] Link `main.css`
- [x] Configure app URLs
- [x] Verify static file structure

---

# 🚀 Part 03 Completed

The main commands and Django template syntax used in **Part 03 - Templates** have been documented here for quick revision.