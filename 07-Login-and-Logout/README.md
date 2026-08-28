# Django Tutorial – Video 7: Login and Logout

This project is part of the **Corey Schafer Django Tutorial** series.

## Features

- User registration
- User login
- User logout
- Authentication-aware navigation
- Profile page
- Django messages
- Crispy Forms with Bootstrap 4
- User profile image support
- Media file configuration

## Project Structure

```text
07-Login-and-Logout/
└── django_project/
    ├── blog/
    ├── users/
    │   ├── migrations/
    │   ├── templates/
    │   ├── forms.py
    │   ├── models.py
    │   └── views.py
    ├── django_project/
    ├── media/
    ├── db.sqlite3
    └── manage.py
```

## Main Concepts

### Django Authentication

Django's built-in authentication system handles login, logout, authentication checks, and protected views.

```django
{% if user.is_authenticated %}
```

### Registration

`UserRegisterForm` is used to create users. After successful registration, the user is redirected to the login page.

### Login

Django's built-in `LoginView` is used with:

```python
auth_views.LoginView.as_view(
    template_name='users/login.html'
)
```

### Logout

Because the project uses a newer Django version than the original tutorial, logout is handled with a POST request.

### Profile

The profile view is protected with:

```python
@login_required
def profile(request):
    return render(request, 'users/profile.html')
```

### Crispy Forms

The project uses:

- `django-crispy-forms`
- `crispy-bootstrap4`

### Media Files

```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

## Important Settings

```python
CRISPY_ALLOWED_TEMPLATE_PACKS = "bootstrap4"
CRISPY_TEMPLATE_PACK = "bootstrap4"

LOGIN_REDIRECT_URL = 'blog-home'
LOGIN_URL = 'login'

MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

## Installation

```powershell
.\.venv\Scripts\Activate.ps1
python -m pip install Pillow
python -m pip install django-crispy-forms
python -m pip install crispy-bootstrap4
```

## Migrations

```powershell
python manage.py makemigrations
python manage.py migrate
```

## Run Project

```powershell
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/
```

## URLs

| URL | Purpose |
|---|---|
| `/` | Blog home |
| `/about/` | About page |
| `/register/` | User registration |
| `/login/` | User login |
| `/logout/` | User logout |
| `/profile/` | User profile |
| `/admin/` | Django admin |

## Django Version Compatibility

This project follows an older tutorial while using a newer Django version. Some authentication behavior differs from the original tutorial.

In particular, logout is handled through a POST form to avoid the HTTP 405 error caused by using a GET request with newer Django versions.

## Status

**Video 7 – Login and Logout: Completed**

Next: Continue with the next tutorial video.
