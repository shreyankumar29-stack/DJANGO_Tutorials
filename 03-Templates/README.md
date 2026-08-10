# Part 03 - Templates 🚀

A comprehensive Django learning project created while following the **Corey Schafer Django Tutorial Series**.

This part focuses on understanding **Django Templates, Template Inheritance, Static Files, Bootstrap, Context Data, and building the initial Blog layout**.

This repository serves as my personal **Django study and revision guide**. It contains the code written during the tutorial, along with detailed documentation, notes, debugging solutions, and modern Django compatibility updates.

The primary purpose of this project is **learning and revision**, not production deployment.

---

# 📚 Topics Covered

### Django Templates

- Django Template System
- `render()`
- Template Variables
- Template Loops
- Passing Context from Views
- Template Inheritance

### Template Inheritance

- `base.html`
- `{% extends %}`
- `{% block %}`
- Reusable Templates
- Child Templates

### Static Files

- Static Files
- CSS Integration
- `{% load static %}`
- `{% static %}`
- Django Static Files Structure

### Frontend

- Bootstrap
- Bootstrap Navbar
- Bootstrap Grid System
- Responsive Layout
- Sidebar

### Blog Layout

- Blog Posts
- Author Information
- Post Dates
- Post Content
- Sidebar
- Home Page
- About Page

---

# 📝 What I Learned

- How Django renders HTML templates.
- How to use the `render()` function.
- How to pass data from a view to a template.
- How Django Template Language works.
- How to use template variables.
- How to use `{% for %}` loops.
- How Template Inheritance works.
- How to create a reusable `base.html`.
- How `{% extends %}` works.
- How `{% block %}` works.
- How to add CSS using Django Static Files.
- How to organize the `static` directory.
- How to integrate Bootstrap with Django.
- How to create a structured blog layout.

---

# 🛠️ Tech Stack

- Python 3
- Django
- HTML5
- CSS3
- Bootstrap
- Django Template Language
- SQLite
- VS Code

---

# 📂 Project Structure

```text
03-Templates/

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
│       │
│       ├── migrations/
│       │
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
├── README.md
├── NOTES.md
└── COMMANDS.md
```

---

# 🔄 Django Request Flow

The basic flow learned in this part:

```text
Browser
   │
   ▼
Project urls.py
   │
   ▼
blog/urls.py
   │
   ▼
views.py
   │
   │ Context
   ▼
Template
   │
   ▼
base.html
   │
   ├── Bootstrap
   ├── CSS
   ├── Navbar
   └── Sidebar
   │
   ▼
Final HTML
   │
   ▼
Browser
```

---

# 🎨 Template Inheritance

A common layout is created inside:

```text
base.html
```

Child templates can reuse it using:

```django
{% extends "blog/base.html" %}
```

Page-specific content is placed inside:

```django
{% block content %}

{% endblock content %}
```

This prevents unnecessary repetition of HTML code.

---

# 📁 Static Files

Static files are organized as:

```text
blog/
└── static/
    └── blog/
        └── main.css
```

The CSS file is loaded using:

```django
{% load static %}
```

and:

```html
<link rel="stylesheet" href="{% static 'blog/main.css' %}">
```

---

# 🐛 Debugging

During this part, a static file error occurred:

```text
'blog\main.css' could not be found
```

The issue was caused by an incorrect/missing static file structure.

The correct structure is:

```text
blog/
└── static/
    └── blog/
        └── main.css
```

After correcting the structure, Django successfully loaded the CSS.

---

# 🎯 Learning Goals

The purpose of this part is to:

- Understand Django's template system.
- Learn Template Inheritance.
- Create reusable layouts.
- Understand static file handling.
- Connect views with templates.
- Build the initial Blog interface.
- Understand how Bootstrap works with Django.
- Prepare for database-backed blog posts in upcoming parts.

---

# 📖 Documentation

Detailed documentation for this part is available in:

### Notes

```text
NOTES.md
```

Contains:

- Detailed explanations
- Concepts
- Template flow
- Template inheritance
- Static files
- Debugging
- Best practices
- Interview questions
- Practice questions

### Commands

```text
COMMANDS.md
```

Contains:

- Django commands
- Server commands
- Static file testing
- Important configuration commands

---

# ⚠️ Note

This project is intended for **learning and revision purposes**.

The blog posts in this stage are temporary data stored inside Python code. Database models will be introduced in later parts of the tutorial.

The tutorial code is based on Corey Schafer's Django Tutorial Series, with modern Django compatibility considered where required.

---

# 📚 Learning Resource

**Tutorial Series:**

Corey Schafer – Django Tutorial Series (YouTube)

---

# ⭐ Repository Highlights

- Django Template System
- Template Inheritance
- Static Files
- Bootstrap Integration
- Blog Layout
- Context Data
- Dynamic Templates
- Detailed Documentation
- Debugging Solutions
- Modern Django Compatibility
- Interview Preparation

---

# 🚀 Future Plans

Continue following the Corey Schafer Django Tutorial Series and gradually transform the initial blog into a complete Django application.

Future topics will include:

- Database Models
- Django ORM
- User Authentication
- Forms
- CRUD Operations
- User Profiles
- Pagination
- Blog Post Management
- Advanced Django Features

---

Happy Learning! 🚀