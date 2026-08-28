# Commands – Video 7: Login and Logout

## Activate Virtual Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

## Install Required Packages

```powershell
python -m pip install Pillow
python -m pip install django-crispy-forms
python -m pip install crispy-bootstrap4
```

## Create Users App

```powershell
python manage.py startapp users
```

## Create Migrations

```powershell
python manage.py makemigrations
```

Or for a specific app:

```powershell
python manage.py makemigrations blog
python manage.py makemigrations users
```

## Apply Migrations

```powershell
python manage.py migrate
```

## Create Superuser

```powershell
python manage.py createsuperuser
```

## Run Development Server

```powershell
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/
```

## Check Django Project

```powershell
python manage.py check
```

## Show Migrations

```powershell
python manage.py showmigrations
```

## Open Django Shell

```powershell
python manage.py shell
```

## Update Requirements

```powershell
python -m pip freeze > requirements.txt
```

## Git Commands

Check changes:

```powershell
git status
```

Stage changes:

```powershell
git add .
```

Commit:

```powershell
git commit -m "Complete Video 7 login and logout"
```

Push:

```powershell
git push
```

## Video 7 Notes

- Pillow is required for `ImageField`.
- Crispy Forms is used for form styling.
- `crispy-bootstrap4` provides Bootstrap 4 support for Crispy Forms.
- Django authentication handles login and logout.
- In the current Django version, logout is handled using a POST form.
- `LOGIN_URL` defines the login URL.
- `LOGIN_REDIRECT_URL` defines where users go after login.
- `MEDIA_ROOT` stores uploaded media.
- `MEDIA_URL` defines the URL prefix for media files.
