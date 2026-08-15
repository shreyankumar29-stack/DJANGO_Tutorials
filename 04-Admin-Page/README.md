# Django Tutorial - Part 04: Admin Page 🚀

A Django learning project created while following the **Corey Schafer Django Tutorial Series**.

This part focuses on understanding the **Django Admin Interface**, registering models with the admin site, managing application data, and continuing the Django Blog project.

The original Corey Schafer tutorial uses an older Django version, so the code in this repository is adapted where necessary to remain compatible with modern Django versions.

---

# 📚 Repository Purpose

This repository is part of my personal Django learning journey.

The purpose of this part is to:

- Understand the Django Admin Interface.
- Learn how Django manages application data.
- Understand how models can be registered with the admin site.
- Practice Django project and app structure.
- Continue building the Blog application.
- Debug common Django errors.
- Maintain modern Django-compatible code.
- Keep detailed documentation for revision.

---

# 📖 Topics Covered

### Django Admin

- Django Admin Interface
- Admin Site
- Registering Models
- Admin Model Management
- Creating a Superuser
- Admin Login
- Managing Application Data

### Django Project Structure

- `manage.py`
- Project package
- Django application
- `settings.py`
- `urls.py`
- `views.py`
- `models.py`
- `admin.py`
- `apps.py`

### URLs & Views

- URL routing
- `include()`
- App-level URLs
- Function-based Views
- Named URLs

### Templates

- `base.html`
- Template inheritance
- `{% extends %}`
- `{% block %}`
- Template rendering
- Context data

### Static Files

- CSS
- `STATIC_URL`
- `{% load static %}`
- `{% static %}`
- App-level static files

### Debugging

- URL 404 errors
- Missing View functions
- Static file 404 errors
- CSRF verification errors
- Django project structure issues

---

# 🛠️ Tech Stack

- Python 3
- Django
- SQLite
- HTML5
- CSS3
- Bootstrap
- VS Code
- Git
- GitHub

---

# 📂 Project Structure

```text
04-Admin-Page/
│
├── django_project/
│   │
│   ├── manage.py
│   │
│   ├── django_project/
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── asgi.py
│   │   └── wsgi.py
│   │
│   └── blog/
│       ├── migrations/
│       ├── static/
│       │   └── blog/
│       │       └── main.css
│       │
│       ├── templates/
│       │   └── blog/
│       │       ├── base.html
│       │       ├── home.html
│       │       └── about.html
│       │
│       ├── __init__.py
│       ├── admin.py
│       ├── apps.py
│       ├── models.py
│       ├── tests.py
│       ├── urls.py
│       └── views.py
│
└── README.md