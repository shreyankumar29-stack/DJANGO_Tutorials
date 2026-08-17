# Part 06 - User Registrations 🚀

A comprehensive Django learning project created while following the **Corey Schafer Django Tutorial Series**.

This part focuses on building a **User Registration system** for the Django Blog application and understanding Django Forms, user creation, validation, CSRF protection, and database integration.

This repository serves as my personal **Django study and revision guide**. It contains the tutorial code, documentation, debugging solutions, and modern Django compatibility updates.

The primary purpose of this project is **learning and revision**, not production deployment.

---

# 📚 Repository Purpose

This part was created to:

- Understand Django's built-in authentication system.
- Build a user registration page.
- Work with Django Forms.
- Validate user input.
- Create users using Django's built-in `User` model.
- Handle POST requests and CSRF protection.
- Understand registration and database integration.
- Debug database and migration issues.
- Maintain a structured Django learning project.

---

# 📖 Topics Covered

### User Registration

- Django Authentication System
- User Registration
- Built-in `User` Model
- User Creation
- User Validation
- Registration Workflow

### Django Forms

- Django Forms
- Form Fields
- Form Validation
- Form Rendering
- POST Requests
- CSRF Protection
- Form Submission

### Database

- SQLite
- Django ORM
- QuerySets
- User Records
- Post Records
- Migrations
- Migration State

### Templates

- Registration Template
- Template Inheritance
- Base Template
- Form Rendering
- Validation Errors

### Debugging

- `ModuleNotFoundError`
- Missing App
- Missing Database Table
- Existing Table During Migration
- Empty QuerySets
- Fresh Database Setup

---

# 📝 What I Learned

- How Django's built-in authentication system is used for user management.
- How to create a registration form.
- How Django validates submitted form data.
- How POST requests are processed.
- Why CSRF protection is required for POST forms.
- How registered users are stored in the database.
- How Django migrations create database tables.
- How to diagnose `no such table` errors.
- How to handle a migration conflict where a table already exists.
- Why a new tutorial part can have an empty database even when previous parts contain data.

---

# 🛠️ Tech Stack

- Python 3
- Django
- Django Authentication
- Django Forms
- Django ORM
- SQLite
- HTML5
- CSS3
- Bootstrap
- VS Code
- Git
- GitHub

---

# 📂 Repository Structure

```text
06-User-Registrations/

├── django_project/
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
│       ├── templates/
│       ├── __init__.py
│       ├── admin.py
│       ├── apps.py
│       ├── forms.py
│       ├── models.py
│       ├── tests.py
│       ├── urls.py
│       └── views.py
│
├── README.md
├── NOTES.md
└── COMMANDS.md
```

---

# 🔐 User Registration Workflow

The basic registration flow is:

```text
Registration Page
       ↓
User fills Form
       ↓
POST Request
       ↓
Form Validation
       ↓
Create User
       ↓
Save to Database
       ↓
Redirect / Continue
```

---

# 🧩 Django Forms

Django Forms provide a structured way to collect and validate user input.

A registration form can contain:

```text
Username
Email
Password
Password Confirmation
```

The form validates the submitted data before creating a user.

---

# 🛡️ CSRF Protection

Django protects POST forms using CSRF protection.

Example:

```django
<form method="POST">
    {% csrf_token %}

    <!-- Form fields -->

    <button type="submit">
        Register
    </button>
</form>
```

The `{% csrf_token %}` tag is required for Django's CSRF protection on POST forms.

---

# 🗄️ Database & Migrations

The User Registration system depends on database tables.

Normal migration workflow:

```text
Model Changes
     ↓
makemigrations
     ↓
Migration Files
     ↓
migrate
     ↓
Database
```

Commands:

```bash
python manage.py makemigrations
```

```bash
python manage.py migrate
```

---

# 🐛 Debugging Experience

### 1. `ModuleNotFoundError: No module named 'blog'`

This happened when `blog.apps.BlogConfig` was already registered in `INSTALLED_APPS`, but the `blog` app had not been created yet.

The app was created first:

```bash
python manage.py startapp blog
```

and then registered in `INSTALLED_APPS`.

---

### 2. `no such table: blog_post`

This occurred when the application tried to query the `Post` model but the current database did not contain the `blog_post` table.

The migration workflow was required:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

### 3. `table "blog_post" already exists`

This occurred when the SQLite database already contained `blog_post`, while Django still considered `blog.0001_initial` unapplied.

For a fresh learning project with no important data, resetting the Part 06 SQLite database and running migrations again gives a clean migration state.

---

### 4. Empty QuerySets

A new tutorial part can have its own database.

Therefore:

```python
User.objects.all()
```

may return:

```text
<QuerySet []>
```

and:

```python
Post.objects.all()
```

may also return:

```text
<QuerySet []>
```

This simply means the current Part 06 database has no matching records.

Data from Part 05 does not automatically transfer to Part 06 when the parts use separate SQLite databases.

---

# 🎯 Learning Goals

The purpose of this part is to:

- Understand Django user registration.
- Learn Django Forms.
- Handle POST requests.
- Validate user input.
- Use Django's built-in authentication system.
- Store registered users in the database.
- Understand migration/database consistency.
- Prepare for login and logout functionality in later parts.

---

# ⭐ Repository Highlights

- User Registration
- Django Authentication
- Django Forms
- Form Validation
- CSRF Protection
- Built-in User Model
- Database Integration
- Django ORM
- Migration Workflow
- Detailed Debugging
- Modern Django Compatibility

---

# 📖 Documentation

This part contains:

### README.md

Part overview, topics, learning goals, project structure, and debugging summary.

### NOTES.md

Detailed explanations, concepts, registration workflow, forms, authentication, database and migration debugging, interview questions, and revision material.

### COMMANDS.md

Django management commands, migration commands, shell commands, debugging commands, and Git commands.

---

# ⚠️ Note

This project is intended for **learning and revision purposes**.

The implementation follows the Corey Schafer Django Tutorial Series while updating code where required for compatibility with the modern Django environment.

The original tutorial uses older Django conventions, so some configuration and generated files may differ from the current Django version.

---

# 📚 Learning Resource

**Tutorial Series:**

Corey Schafer – Django Tutorial Series (YouTube)

---

# 🚀 Future Plans

Continue developing the Django Blog application by adding:

- User Login
- User Logout
- Authentication
- User Profiles
- Password Management
- Blog Post Ownership
- User-specific Features

The overall goal is to gradually transform the tutorial Blog into a complete Django application.

---

Happy Learning! 🚀
