# Part 02 - Applications & Routes 🚀

In this part of the Django tutorial series, we create our first Django application and learn how requests travel through Django before reaching the browser.

This is one of the most important parts of Django because it introduces the concepts of **Apps, Views, URL Routing, and HTTP Responses**.

---

# 📚 Topics Covered

- Creating a Django App
- Understanding Django Apps
- Project vs App
- Views
- URL Routing
- Project URLs
- App URLs
- HttpResponse
- include()
- Request & Response Cycle

---

# 📝 What I Learned

- Difference between a Django Project and a Django App.
- How to create a new app using `startapp`.
- Purpose of `views.py`.
- How URL routing works in Django.
- Why we create a separate `urls.py` inside each app.
- How Django processes a browser request.
- How `HttpResponse` returns data to the browser.

---

# 🛠️ Commands Used

## Create App

```bash
python manage.py startapp blog
```

---

## Run Development Server

```bash
python manage.py runserver
```

---

# 📂 Project Structure

```text
django_project/

│── manage.py

├── django_project/
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   └── wsgi.py
│
└── blog/
    ├── migrations/
    ├── __init__.py
    ├── admin.py
    ├── apps.py
    ├── models.py
    ├── tests.py
    ├── urls.py
    └── views.py
```

---

# 🎯 Key Takeaways

- A Django project can contain multiple apps.
- Each app should have its own responsibility.
- URLs are responsible for directing requests.
- Views process requests and return responses.
- `include()` keeps URL configuration modular.
- `HttpResponse` sends data back to the browser.

---

# ⚠️ Note

This part focuses only on understanding the routing system of Django.

No database or models are used yet.

---

Happy Learning! 🚀