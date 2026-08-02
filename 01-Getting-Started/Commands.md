# Part 01 - Commands Reference

This file contains all the commands used in Part 01 of the Django tutorial series.

---

# Create a Virtual Environment

```bash
python -m venv .venv
```

Creates an isolated Python environment for the project.

---

# Activate Virtual Environment (PowerShell)

```powershell
.venv\Scripts\Activate.ps1
```

Activates the virtual environment.

---

# Activate Virtual Environment (Command Prompt)

```cmd
.venv\Scripts\activate
```

Activates the virtual environment in Command Prompt.

---

# Install Django

```bash
pip install django
```

Installs the latest Django version.

---

# Check Django Version

```bash
django-admin --version
```

Displays the installed Django version.

---

# Create a Django Project

```bash
django-admin startproject django_project .
```

Creates a new Django project in the current directory.

---

# Run Development Server

```bash
python manage.py runserver
```

Starts Django's development server.

---

# Stop Development Server

```text
CTRL + C
```

Stops the running server.