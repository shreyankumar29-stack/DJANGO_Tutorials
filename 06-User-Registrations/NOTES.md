# Part 06 — User Registrations — NOTES.md

Notes for **Part 06 of the Corey Schafer Django Tutorial Series**.

---

## 1. User Registration

Django provides a built-in authentication system for managing users.

### Registration Flow

```text
User
 ↓
Registration Form
 ↓
Form Validation
 ↓
UserCreationForm
 ↓
User Model
 ↓
Database
```

---

## 2. UserCreationForm

Django provides `UserCreationForm` for creating users.

```python
from django.contrib.auth.forms import UserCreationForm
```

Custom registration form:

```python
from django import forms
from django.contrib.auth.models import User
from django.contrib.auth.forms import UserCreationForm


class UserRegisterForm(UserCreationForm):
    email = forms.EmailField()

    class Meta:
        model = User
        fields = ['username', 'email', 'password1', 'password2']
```

### Fields

| Field | Purpose |
|---|---|
| `username` | User's username |
| `email` | User's email |
| `password1` | Password |
| `password2` | Password confirmation |

---

## 3. Django Forms

Django Forms are used for:

- Collecting user input
- Validating data
- Processing submitted data
- Displaying validation errors

### Request Flow

```text
GET
 ↓
Display Form
 ↓
POST
 ↓
Validate Form
 ↓
Save Data
```

---

## 4. CSRF Protection

Django protects POST forms using CSRF tokens.

```django
{% csrf_token %}
```

Example:

```django
<form method="POST">
    {% csrf_token %}

    {{ form|crispy }}

    <button type="submit">Sign Up</button>
</form>
```

**CSRF** = Cross-Site Request Forgery.

---

## 5. Crispy Forms

Crispy Forms simplifies Django form rendering and styling.

### Installation

```bash
pip install django-crispy-forms
pip install crispy-bootstrap4
```

### settings.py

```python
INSTALLED_APPS = [
    'crispy_forms',
    'crispy_bootstrap4',
]
```

```python
CRISPY_ALLOWED_TEMPLATE_PACKS = 'bootstrap4'
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

### Template

```django
{% load crispy_forms_tags %}

{{ form|crispy }}
```

---

## 6. Users App

The `users` app handles authentication-related functionality.

### Structure

```text
users/
├── migrations/
├── templates/
│   └── users/
│       ├── login.html
│       └── register.html
├── apps.py
├── forms.py
├── models.py
└── views.py
```

Correct app configuration:

```python
'users.apps.UsersConfig'
```

`UsersConfig` is defined in:

```text
users/apps.py
```

---

## 7. forms.py

`forms.py` is created manually inside the `users` app.

```python
from django import forms
from django.contrib.auth.models import User
from django.contrib.auth.forms import UserCreationForm


class UserRegisterForm(UserCreationForm):
    email = forms.EmailField()

    class Meta:
        model = User
        fields = ['username', 'email', 'password1', 'password2']
```

---

## 8. Django User Model

Django provides a built-in `User` model.

```python
from django.contrib.auth.models import User
```

Get all users:

```python
User.objects.all()
```

Get a specific user:

```python
User.objects.get(username='Shreyansh')
```

Create a user:

```python
User.objects.create_user(
    username='Shreyansh',
    email='shreyansh@example.com',
    password='TestPassword123'
)
```

### Important

Use `create_user()` because Django handles password hashing.

---

## 9. Migrations

Migrations synchronize Django models with the database.

### Migration Flow

```text
models.py
    ↓
makemigrations
    ↓
Migration File
    ↓
migrate
    ↓
Database
```

Create migrations:

```bash
python manage.py makemigrations
```

Apply migrations:

```bash
python manage.py migrate
```

Check migrations:

```bash
python manage.py showmigrations
```

---

## 10. Django Shell

Start:

```bash
python manage.py shell
```

Import User:

```python
from django.contrib.auth.models import User
```

Example:

```python
User.objects.all()
```

Exit:

```python
exit()
```

---

## 11. Superuser

A superuser can access the Django admin panel.

Create:

```bash
python manage.py createsuperuser
```

Admin:

```text
http://127.0.0.1:8000/admin/
```

---

## 12. Important URLs

### Home

```text
http://127.0.0.1:8000/
```

### Registration

```text
http://127.0.0.1:8000/register/
```

### Admin

```text
http://127.0.0.1:8000/admin/
```

---

## 13. Registration Workflow

```text
User
 ↓
/register/
 ↓
Registration Form
 ↓
POST Request
 ↓
UserRegisterForm
 ↓
Validation
 ↓
UserCreationForm
 ↓
User Model
 ↓
Database
```

---

## 14. Debugging

Useful command:

```bash
python manage.py check
```

### Debugging Workflow

```text
Read Error
    ↓
Find File + Line
    ↓
Identify Problem
    ↓
Fix Problem
    ↓
python manage.py check
    ↓
python manage.py runserver
```

---

## 15. Common Errors

### `ModuleNotFoundError: No module named 'users.app'`

Wrong:

```python
'users.app.UsersConfig'
```

Correct:

```python
'users.apps.UsersConfig'
```

---

### `crispy_forms_tags is not a registered tag library`

Install:

```bash
pip install django-crispy-forms
```

Add:

```python
'crispy_forms',
```

to `INSTALLED_APPS`.

---

### `TemplateDoesNotExist: bootstrap4/uni_form.html`

Install:

```bash
pip install crispy-bootstrap4
```

Add:

```python
'crispy_bootstrap4',
```

and configure:

```python
CRISPY_ALLOWED_TEMPLATE_PACKS = 'bootstrap4'
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

---

### `ModuleNotFoundError: No module named 'users.forms'`

Create:

```text
users/forms.py
```

and define `UserRegisterForm`.

---

## 16. Key Concepts

| Concept | Purpose |
|---|---|
| `UserCreationForm` | Built-in form for creating users |
| `UserRegisterForm` | Custom registration form |
| `EmailField` | Adds email input and validation |
| `csrf_token` | Protects POST forms |
| `crispy_forms` | Form rendering |
| `crispy-bootstrap4` | Bootstrap 4 support |
| `makemigrations` | Creates migration files |
| `migrate` | Applies migrations |
| `create_user()` | Creates user with hashed password |
| `createsuperuser` | Creates admin account |

---

## 17. Key Takeaways

- Django provides a built-in authentication system.
- `UserCreationForm` simplifies user registration.
- Custom forms can extend Django's built-in forms.
- `forms.py` is created manually.
- CSRF protection is required for POST forms.
- Crispy Forms simplifies form rendering.
- Migrations synchronize models with the database.
- Django's built-in `User` model manages users.
- `create_user()` should be used to create users.
- Superusers can access the Django admin panel.
- `python manage.py check` is useful for debugging.

---

# Part 06 Completed

- [x] User Registration
- [x] Django Forms
- [x] UserCreationForm
- [x] Custom UserRegisterForm
- [x] Email Field
- [x] Form Validation
- [x] CSRF Protection
- [x] Crispy Forms
- [x] Bootstrap 4
- [x] Django User Model
- [x] Django ORM
- [x] Migrations
- [x] Superuser
- [x] Debugging

---

## Tutorial

**Corey Schafer — Django Tutorial Series**

**Part 06 — User Registrations**
