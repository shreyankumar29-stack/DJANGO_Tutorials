# Part 02 - Applications & Routes 📝

---

# 🎯 Objective

The goal of this video is to understand how Django handles a browser request and how a Django application is created.

By the end of this tutorial you should understand:

- Project
- App
- URL Routing
- Views
- HttpResponse
- Request Flow

---

# 1️⃣ What is a Django App?

A Django App is a self-contained module that performs a specific task inside a Django project.

Example:

College Management System

```
Authentication
Attendance
Library
Fees
Students
```

Each feature is created as an individual Django App.

Corey creates a Blog App.

---

# 2️⃣ Creating an App

Command:

```bash
python manage.py startapp blog
```

This command creates the following files automatically:

```
blog/

admin.py
apps.py
models.py
tests.py
views.py
migrations/
```

---

# 3️⃣ Explanation of Every File

## views.py

Contains business logic.

Whenever a user visits a webpage, Django executes a View.

Example

```python
def home(request):
    return HttpResponse("Blog Home")
```

---

## models.py

Stores database models.

Example:

Post

Comment

User Profile

In this video we do NOT use models.

---

## admin.py

Registers models inside Django Admin.

Not used in this video.

---

## apps.py

Stores application configuration.

Normally we don't modify this file.

---

## migrations/

Stores database migration files.

No migration is created yet.

---

# 4️⃣ Project vs App

Project

Entire Website

↓

Apps

Authentication

Blog

Payments

Attendance

Library

Think of a Project as a "Company"

Apps are different "Departments".

---

# 5️⃣ URL Routing

Django follows a routing system.

Browser

↓

Project urls.py

↓

App urls.py

↓

View

↓

Response

---

# 6️⃣ Project urls.py

Project urls.py works like the Main Reception.

It receives every request first.

Example

```python
path("blog/", include("blog.urls"))
```

Meaning

Whenever someone visits

```
localhost:8000/blog/
```

send the request to Blog App.

---

# 7️⃣ App urls.py

Inside blog/urls.py

```python
urlpatterns = [
    path("", views.home),
]
```

Meaning

If user visits

```
blog/
```

call

```
views.home()
```

---

# 8️⃣ View

Example

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("<h1>Blog Home</h1>")
```

Request comes from browser.

↓

View executes.

↓

Returns HttpResponse.

↓

Browser displays output.

---

# 9️⃣ HttpResponse

HttpResponse sends data back to the browser.

Example

```
Blog Home
```

Later we replace HttpResponse with HTML Templates.

---

# 🔟 Complete Request Flow

```
Browser

↓

Project urls.py

↓

App urls.py

↓

View

↓

HttpResponse

↓

Browser
```

This flow is the backbone of Django.

---

# Real-Life Example

Imagine a Shopping Mall.

Customer enters.

↓

Security Guard

↓

Sends customer to correct shop.

↓

Shopkeeper serves customer.

↓

Customer receives product.

Mapping:

Customer → Browser

Security Guard → Project urls.py

Shop → App urls.py

Shopkeeper → View

Product → HttpResponse

---

# Modern Django Notes

Corey Schafer's routing code is still compatible with the latest Django.

However, always use

```python
path()
```

instead of older

```python
url()
```

which has been removed from modern Django.

---

# Common Errors

## Error

```
ImportError: cannot import name 'Post'
```

Reason

Trying to import Post before creating the Post model.

Solution

Remove

```python
from .models import Post
```

until the model is created in later tutorials.

---

## Error

```
ModuleNotFoundError
```

Reason

Wrong app name.

---

## Error

```
No module named blog.urls
```

Reason

urls.py not created inside blog app.

---

## Error

```
Page not found (404)
```

Reason

Incorrect URL mapping.

---

# Best Practices

- Keep one responsibility per app.
- Use separate urls.py for every app.
- Don't put all URLs in the project urls.py.
- Keep views simple.
- Follow Django's default structure.

---

# Interview Questions

- What is a Django App?
- Difference between Project and App?
- What is URL Routing?
- What is HttpResponse?
- Why do we use include()?
- What is the purpose of views.py?
- Explain Django Request Flow.

---

# Practice Questions

1. Create an app named students.
2. Create an app named accounts.
3. Create two views.
4. Configure URLs.
5. Display two different pages.

---

# Revision Summary

✔ Created first Django App

✔ Learned Project vs App

✔ Learned URL Routing

✔ Learned Views

✔ Learned HttpResponse

✔ Understood Complete Request Flow

✔ Ready for Templates in upcoming videos.