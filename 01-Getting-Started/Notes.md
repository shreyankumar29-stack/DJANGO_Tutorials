# Part 01 - Notes 📝

## What is Django?

Django is a high-level Python web framework that allows developers to build secure, scalable, and maintainable web applications quickly.

It follows the **MVT (Model-View-Template)** architecture.

---

# Django Project vs Django App

## Django Project

A project is the entire web application.

Example:

```
College Management System
```

Inside one project, multiple apps can exist.

---

## Django App

An app is a specific module responsible for a single functionality.

Examples:

- Authentication
- Blog
- Attendance
- Payments

One Django project can contain multiple apps.

---

# Virtual Environment

A virtual environment creates an isolated Python environment for a project.

Benefits:

- Prevents package conflicts.
- Different projects can use different package versions.
- Keeps global Python installation clean.

---

# manage.py

Purpose:

- Run development server.
- Create apps.
- Perform migrations.
- Open Django shell.
- Execute management commands.

Common Commands:

```bash
python manage.py runserver
python manage.py startapp blog
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
```

---

# settings.py

Contains all project configuration.

Examples:

- Installed Apps
- Database
- Middleware
- Templates
- Static Files
- Secret Key
- Time Zone

Almost every Django project requires modifications in this file.

---

# urls.py

Responsible for routing URLs.

Example:

```
/home
/about
/contact
```

Every incoming request first reaches urls.py.

---

# asgi.py

Full Form:

Asynchronous Server Gateway Interface

Purpose:

- Supports asynchronous programming.
- Used for WebSockets.
- Required for real-time applications.
- Used by ASGI servers like Uvicorn and Daphne.

Normally developers do not modify this file during beginner-level projects.

---

# wsgi.py

Full Form:

Web Server Gateway Interface

Purpose:

- Used during deployment.
- Connects Django with web servers.
- Supports traditional synchronous applications.

Usually not modified during beginner tutorials.

---

# __init__.py

Marks the directory as a Python package.

Usually remains empty.

---

# Development Server

Run:

```bash
python manage.py runserver
```

Default URL:

```
http://127.0.0.1:8000/
```

Stop server:

```
CTRL + C
```

---

# Modern Django Best Practices

- Use `.venv` as the virtual environment name.
- Keep the virtual environment outside version control.
- Add `.venv/` to `.gitignore`.
- Use `python -m pip install` when needed.
- Freeze dependencies using:

```bash
pip freeze > requirements.txt
```

---

# Common Beginner Mistakes

❌ Running commands outside the project folder.

❌ Forgetting to activate the virtual environment.

❌ Confusing Project with App.

❌ Editing `asgi.py` or `wsgi.py` unnecessarily.

❌ Forgetting to install Django inside the virtual environment.

---

# Interview Questions

### What is Django?

### What is a virtual environment?

### Difference between Project and App?

### What is manage.py?

### What is settings.py?

### What is urls.py?

### Difference between ASGI and WSGI?

### What is the purpose of __init__.py?

---

# Revision Summary

✔ Django Project Created

✔ Virtual Environment Configured

✔ Development Server Started

✔ Project Structure Understood

✔ Default Configuration Files Learned

✔ Ready to Create First Django App