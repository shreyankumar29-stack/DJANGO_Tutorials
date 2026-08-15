# Django Tutorial - Part 04: Admin Page 🛠️

Complete command reference for **Part 04 of the Corey Schafer Django Tutorial Series**.

This file contains the commands used for:

- Virtual Environment
- Django Server
- Django Admin
- Superuser
- App Creation
- Migrations
- Django Checks
- Static Files
- Git & GitHub
- Useful debugging commands

---

# 📁 Project Location

For Part 04, the project structure is:

```text
DJANGO_Tutorials/
│
├── .venv/
│
└── 04-Admin-Page/
    │
    └── django_project/
        │
        ├── manage.py
        │
        ├── django_project/
        │
        └── blog/
```

All Django `manage.py` commands should normally be executed from the directory containing:

```text
manage.py
```

---

# 🐍 1. Virtual Environment

## Activate Virtual Environment

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

After activation, the terminal should show:

```text
(.venv)
```

Example:

```text
(.venv) PS C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials>
```

---

## Activate Virtual Environment - CMD

If using Command Prompt:

```cmd
.venv\Scripts\activate
```

---

## Deactivate Virtual Environment

```powershell
deactivate
```

---

# 🐍 2. Check Python

Check installed Python version:

```powershell
python --version
```

Example:

```text
Python 3.14.x
```

---

# 📦 3. Check pip

```powershell
pip --version
```

---

# 📦 4. Install Django

If Django is not installed inside the virtual environment:

```powershell
pip install django
```

---

# 🔍 5. Check Django Version

```powershell
python -m django --version
```

Another way:

```powershell
django-admin --version
```

---

# 📋 6. Check Django Package

```powershell
pip show django
```

This displays information such as:

- Package name
- Version
- Installation location
- Dependencies

---

# 🚀 7. Start Django Development Server

Go to the folder containing `manage.py`.

Then run:

```powershell
python manage.py runserver
```

Default development server:

```text
http://127.0.0.1:8000/
```

---

# 🔌 8. Run Server on Another Port

For example:

```powershell
python manage.py runserver 8001
```

Then open:

```text
http://127.0.0.1:8001/
```

---

# 🛑 9. Stop Development Server

Press:

```text
CTRL + C
```

---

# 👤 10. Create Django Superuser

Create an administrator account:

```powershell
python manage.py createsuperuser
```

Django asks for:

```text
Username:
Email address:
Password:
Password (again):
```

After successful creation, the superuser can log into:

```text
http://127.0.0.1:8000/admin/
```

---

# 🌐 11. Important URLs

## Home Page

```text
http://127.0.0.1:8000/
```

---

## About Page

```text
http://127.0.0.1:8000/about/
```

---

## Django Admin

```text
http://127.0.0.1:8000/admin/
```

---

## Static CSS

```text
http://127.0.0.1:8000/static/blog/main.css
```

This URL can be used to check whether Django is serving the CSS file correctly.

---

# 🏗️ 12. Create Django App

If the Blog application does not already exist:

```powershell
python manage.py startapp blog
```

This creates:

```text
blog/
├── migrations/
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── tests.py
└── views.py
```

---

# 🗄️ 13. Database Migrations

## Create Migration Files

```powershell
python manage.py makemigrations
```

This detects changes made to models and creates migration files.

---

## Apply Migrations

```powershell
python manage.py migrate
```

This applies migrations to the database.

---

## Show Migration Status

```powershell
python manage.py showmigrations
```

This displays which migrations have been applied.

---

# 🔎 14. Django System Check

Run:

```powershell
python manage.py check
```

This checks the Django project for common configuration problems.

If everything is correct, Django should report:

```text
System check identified no issues.
```

---

# 🧪 15. Run Development Server After Changes

After making changes to:

- `views.py`
- `urls.py`
- `settings.py`
- `models.py`
- templates
- static files

run:

```powershell
python manage.py runserver
```

Django's development server automatically reloads many code changes.

---

# 🔗 16. Project URL Configuration

File:

```text
django_project/urls.py
```

Example:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('blog.urls')),
]
```

Important commands are not required here, but this configuration determines:

```text
/admin/ → Django Admin
/       → Blog URLs
```

---

# 🔗 17. Blog URL Configuration

File:

```text
blog/urls.py
```

Example:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='blog-home'),
    path('about/', views.about, name='blog-about'),
]
```

This creates:

```text
/        → views.home
/about/  → views.about
```

---

# 🖥️ 18. Basic Views

File:

```text
blog/views.py
```

Example:

```python
from django.shortcuts import render


def home(request):
    return render(request, 'blog/home.html')


def about(request):
    return render(request, 'blog/about.html')
```

---

# 🛠️ 19. Register Model in Admin

File:

```text
blog/admin.py
```

Example:

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

After registering the model:

1. Start the server.
2. Open Admin.
3. Login as superuser.
4. Check whether the model appears.

---

# 🎨 20. Static Files Structure

Correct structure:

```text
blog/
│
└── static/
    │
    └── blog/
        │
        └── main.css
```

The important part is:

```text
static/blog/main.css
```

---

# 🎨 21. Load Static Files

In the template:

```django
{% load static %}
```

Then:

```html
<link rel="stylesheet"
      type="text/css"
      href="{% static 'blog/main.css' %}">
```

---

# 🔍 22. Test Static CSS

Open:

```text
http://127.0.0.1:8000/static/blog/main.css
```

If the CSS content appears in the browser, Django is able to serve the static file.

---

# ⚙️ 23. Static URL Setting

In:

```text
django_project/settings.py
```

make sure:

```python
STATIC_URL = '/static/'
```

exists.

Also make sure:

```python
'django.contrib.staticfiles',
```

is present in:

```python
INSTALLED_APPS
```

---

# 🧩 24. Template Inheritance

Child template:

```django
{% extends "blog/base.html" %}
```

Content block:

```django
{% block content %}

<!-- Page content -->

{% endblock content %}
```

This allows multiple pages to reuse the same base template.

---

# 🛡️ 25. CSRF Token

For POST forms:

```django
<form method="POST">

    {% csrf_token %}

    <!-- Form fields -->

    <button type="submit">
        Submit
    </button>

</form>
```

The CSRF token must be inside the form.

---

# 🚨 26. Fix `views.home` Error

If you get:

```text
AttributeError:
module 'blog.views' has no attribute 'home'
```

Check:

```text
blog/views.py
```

Make sure it contains:

```python
def home(request):
    return render(request, 'blog/home.html')
```

Also check:

```text
blog/urls.py
```

for:

```python
path('', views.home, name='blog-home')
```

---

# 🚨 27. Fix `/home` 404

If your URL is:

```python
path('', views.home, name='blog-home')
```

the correct URL is:

```text
http://127.0.0.1:8000/
```

Not:

```text
http://127.0.0.1:8000/home
```

If you specifically wanted `/home/`, you would need:

```python
path('home/', views.home, name='blog-home')
```

---

# 🚨 28. Fix Static File 404

If Django says:

```text
'blog/main.css' could not be found
```

check the folder structure:

```text
blog/
└── static/
    └── blog/
        └── main.css
```

Then check the template:

```django
{% load static %}
```

and:

```django
{% static 'blog/main.css' %}
```

Finally test:

```text
http://127.0.0.1:8000/static/blog/main.css
```

---

# 🚨 29. Fix CSRF 403

If you see:

```text
Forbidden (403)

CSRF verification failed.
CSRF token missing.
```

check the POST form.

Correct:

```django
<form method="POST">
    {% csrf_token %}

    ...
</form>
```

Do not remove CSRF middleware just to hide the error.

---

# 🔄 30. Restart Server

Normally Django automatically reloads Python code during development.

If something does not update correctly, stop the server:

```text
CTRL + C
```

Then restart:

```powershell
python manage.py runserver
```

---

# 🧹 31. Clear Terminal

Windows CMD / PowerShell:

```powershell
cls
```

---

# 📂 32. Check Current Directory

PowerShell:

```powershell
pwd
```

or:

```powershell
Get-Location
```

---

# 📁 33. List Files

PowerShell:

```powershell
dir
```

or:

```powershell
ls
```

Check whether:

```text
manage.py
```

is present.

If it is not present, move into the correct Django project directory.

---

# 📁 34. Change Directory

Example:

```powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials\04-Admin-Page\django_project"
```

Then check:

```powershell
dir
```

You should see:

```text
manage.py
```

---

# 🧪 35. Useful Django Check Workflow

Before starting the server:

```powershell
python manage.py check
```

If no problems are found:

```powershell
python manage.py runserver
```

This gives a simple workflow:

```text
python manage.py check
        ↓
No errors?
        ↓
python manage.py runserver
        ↓
Open browser
        ↓
Test application
```

---

# 🌐 36. Test Application

After starting the server:

```powershell
python manage.py runserver
```

Test:

```text
Home:
http://127.0.0.1:8000/
```

```text
About:
http://127.0.0.1:8000/about/
```

```text
Admin:
http://127.0.0.1:8000/admin/
```

```text
CSS:
http://127.0.0.1:8000/static/blog/main.css
```

---

# 📦 37. Pip Freeze

To save installed Python packages:

```powershell
pip freeze
```

To save them into `requirements.txt`:

```powershell
pip freeze > requirements.txt
```

---

# 📥 38. Install Requirements

If a `requirements.txt` file exists:

```powershell
pip install -r requirements.txt
```

---

# 🔧 39. Git Commands

## Check Git Status

```powershell
git status
```

---

## Add All Changes

```powershell
git add .
```

---

## Commit Changes

```powershell
git commit -m "Complete Django Part 04"
```

---

## Push to GitHub

```powershell
git push origin main
```

---

## Check Recent Commits

```powershell
git log --oneline -5
```

---

## Check Remote Repository

```powershell
git remote -v
```

---

# 📌 40. GitHub Workflow

After completing Part 04:

```powershell
git status
```

Then:

```powershell
git add .
```

Then:

```powershell
git commit -m "Complete Django Part 04"
```

Finally:

```powershell
git push origin main
```

Complete flow:

```text
Make Changes
     ↓
git status
     ↓
git add .
     ↓
git commit
     ↓
git push
     ↓
GitHub
```

---

# 🗑️ 41. Remove File From Git Tracking

If a file should no longer be tracked:

```powershell
git rm --cached filename
```

For example:

```powershell
git rm --cached .env
```

Then:

```powershell
git commit -m "Remove unwanted file"
```

And:

```powershell
git push origin main
```

---

# 📂 42. Remove Directory From Git Tracking

To remove a directory from Git tracking while keeping it locally:

```powershell
git rm -r --cached directory-name
```

Then:

```powershell
git commit -m "Remove unwanted directory"
```

And:

```powershell
git push origin main
```

---

# 🔎 43. Check Git Tracked Files

```powershell
git ls-files
```

This shows files currently tracked by Git.

---

# 📋 44. Quick Django Command Reference

| Command | Purpose |
|---|---|
| `python manage.py runserver` | Start development server |
| `python manage.py runserver 8001` | Start server on port 8001 |
| `python manage.py check` | Check Django configuration |
| `python manage.py createsuperuser` | Create superuser |
| `python manage.py startapp blog` | Create Blog app |
| `python manage.py makemigrations` | Create migrations |
| `python manage.py migrate` | Apply migrations |
| `python manage.py showmigrations` | Show migration status |
| `python -m django --version` | Check Django version |
| `pip show django` | Show Django package |
| `pip freeze` | Show installed packages |
| `pip freeze > requirements.txt` | Save dependencies |
| `pip install -r requirements.txt` | Install dependencies |
| `CTRL + C` | Stop server |
| `cls` | Clear terminal |

---

# 📋 45. Quick Git Command Reference

| Command | Purpose |
|---|---|
| `git status` | Check repository status |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Create commit |
| `git push origin main` | Push to GitHub |
| `git log --oneline -5` | Show recent commits |
| `git remote -v` | Show remote repository |
| `git ls-files` | Show tracked files |
| `git rm --cached file` | Stop tracking a file |
| `git rm -r --cached folder` | Stop tracking a directory |

---

# 🌐 46. Quick URL Reference

| URL | Purpose |
|---|---|
| `/` | Blog Home |
| `/about/` | About Page |
| `/admin/` | Django Admin |
| `/static/blog/main.css` | Static CSS test |

Full local URLs:

```text
http://127.0.0.1:8000/
```

```text
http://127.0.0.1:8000/about/
```

```text
http://127.0.0.1:8000/admin/
```

```text
http://127.0.0.1:8000/static/blog/main.css
```

---

# 🎯 47. Part 04 Command Checklist

## Environment

- [x] Activate `.venv`
- [x] Check Python
- [x] Check pip
- [x] Check Django

## Django

- [x] Start server
- [x] Stop server
- [x] Run `check`
- [x] Create superuser
- [x] Access Admin
- [x] Create app
- [x] Run migrations

## Static Files

- [x] Check static folder
- [x] Load `{% static %}`
- [x] Test CSS URL

## Debugging

- [x] Debug `views.home`
- [x] Debug `/home` 404
- [x] Debug static file 404
- [x] Debug CSRF 403

## GitHub

- [x] Check Git status
- [x] Add changes
- [x] Commit changes
- [x] Push to GitHub

---

# 🚀 Part 04 Complete

The important commands used during Part 04 have been documented.

Main development workflow:

```text
Activate Virtual Environment
          ↓
python manage.py check
          ↓
python manage.py runserver
          ↓
Test Home / About / Admin
          ↓
Fix Errors
          ↓
git status
          ↓
git add .
          ↓
git commit
          ↓
git push origin main
```

This `COMMANDS.md` will be used as the command reference for **Part 04 - Admin Page**.