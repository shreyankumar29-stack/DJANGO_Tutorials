# Part 06 - User Registrations - COMMANDS.md

Complete command reference for **Part 06 of the Corey Schafer Django Tutorial Series**.

## 1. Virtual Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

```powershell
python --version
python -m django --version
```

## 2. Navigate to Part 06

```powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials\06-User-Registrations\django_project"
```

```powershell
Get-Location
```

## 3. Create Apps

```powershell
python manage.py startapp blog
```

```powershell
python manage.py startapp users
```

## 4. Django System Check

```powershell
python manage.py check
```

## 5. Install Crispy Forms

```powershell
pip install django-crispy-forms
```

```powershell
pip install crispy-bootstrap4
```

Check packages:

```powershell
pip list
```

```powershell
pip show django-crispy-forms
```

```powershell
pip show crispy-bootstrap4
```

## 6. Crispy Forms Configuration

Add to `INSTALLED_APPS`:

```python
'crispy_forms',
'crispy_bootstrap4',
```

Add to `settings.py`:

```python
CRISPY_ALLOWED_TEMPLATE_PACKS = 'bootstrap4'
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

## 7. Migrations

```powershell
python manage.py makemigrations
```

```powershell
python manage.py makemigrations blog
```

```powershell
python manage.py makemigrations users
```

```powershell
python manage.py migrate
```

Check migrations:

```powershell
python manage.py showmigrations
```

```powershell
python manage.py showmigrations blog
```

```powershell
python manage.py showmigrations users
```

## 8. Fresh Database Reset

Only when the Part 06 database is disposable:

```powershell
Remove-Item db.sqlite3
```

Then:

```powershell
python manage.py migrate
```

> Do not delete `db.sqlite3` if it contains important data.

## 9. Django Shell

Start:

```powershell
python manage.py shell
```

Exit:

```python
exit()
```

## 10. User Queries

```python
from django.contrib.auth.models import User
```

```python
User.objects.all()
```

```python
user = User.objects.get(username='Shreyansh')
```

```python
user
```

```python
user.id
```

```python
user.username
```

```python
user.email
```

## 11. Create User Safely

```python
user = User.objects.create_user(
    username='Shreyansh',
    email='shreyansh@example.com',
    password='TestPassword123'
)
```

Verify:

```python
User.objects.all()
```

## 12. Create Superuser

```powershell
python manage.py createsuperuser
```

## 13. Run Server

```powershell
python manage.py runserver
```

Home:

```text
http://127.0.0.1:8000/
```

Registration:

```text
http://127.0.0.1:8000/register/
```

Admin:

```text
http://127.0.0.1:8000/admin/
```

Stop:

```text
CTRL + C
```

## 14. Registration Form

Create:

```text
users/forms.py
```

Example:

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

## 15. Check Project Files

```powershell
Get-ChildItem
```

```powershell
Get-ChildItem users
```

```powershell
Get-ChildItem users\templates\users
```

## 16. Debugging Commands

```powershell
python manage.py check
```

```powershell
python manage.py showmigrations
```

```powershell
python -m django --version
```

```powershell
python --version
```

```powershell
pip list
```

## 17. Common Errors

### `ModuleNotFoundError: No module named 'users.app'`

Incorrect:

```python
'users.app.UsersConfig'
```

Correct:

```python
'users.apps.UsersConfig'
```

### `crispy_forms_tags is not a registered tag library`

Install:

```powershell
pip install django-crispy-forms
```

Add:

```python
'crispy_forms',
```

### `TemplateDoesNotExist: bootstrap4/uni_form.html`

Install:

```powershell
pip install crispy-bootstrap4
```

Add:

```python
'crispy_bootstrap4',
```

and:

```python
CRISPY_ALLOWED_TEMPLATE_PACKS = 'bootstrap4'
CRISPY_TEMPLATE_PACK = 'bootstrap4'
```

### `ModuleNotFoundError: No module named 'users.forms'`

Create:

```text
users/forms.py
```

and define `UserRegisterForm`.

## 18. GitHub Upload

Go to repository root:

```powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
```

Check:

```powershell
git status
```

Stage Part 06:

```powershell
git add "06-User-Registrations"
```

Check staged files:

```powershell
git status
```

Commit:

```powershell
git commit -m "Add Django Part 06 user registrations"
```

Push:

```powershell
git push origin main
```

Latest commit:

```powershell
git log -1 --oneline
```

## 19. Useful Git Commands

```powershell
git branch
```

```powershell
git remote -v
```

```powershell
git log --oneline
```

```powershell
git show --stat --oneline HEAD
```

## 20. Complete Setup Sequence

```powershell
.\.venv\Scripts\Activate.ps1
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials\06-User-Registrations\django_project"
python -m django --version
pip install django-crispy-forms crispy-bootstrap4
python manage.py check
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

## 21. GitHub Sequence

```powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
git status
git add "06-User-Registrations"
git status
git commit -m "Add Django Part 06 user registrations"
git push origin main
```

## ✅ Part 06 Checklist

- [x] Activate virtual environment
- [x] Create/check Django apps
- [x] Install `django-crispy-forms`
- [x] Install `crispy-bootstrap4`
- [x] Configure Crispy Forms
- [x] Run Django checks
- [x] Create and apply migrations
- [x] Use Django shell
- [x] Create users
- [x] Create superuser
- [x] Run development server
- [x] Test `/register/`
- [x] Debug Crispy Forms
- [x] Debug missing `users/forms.py`
- [x] Stage Part 06
- [x] Commit Part 06
- [x] Push Part 06 to GitHub

## 📌 Important

1. Run Django commands from the directory containing `manage.py`.
2. Activate the correct `.venv`.
3. Run `python manage.py check` when debugging.
4. Run `makemigrations` before `migrate` after model changes.
5. Do not delete `db.sqlite3` if it contains important data.
6. `django-crispy-forms` and `crispy-bootstrap4` are separate packages.
7. `users/forms.py` must exist when `users/views.py` imports `UserRegisterForm`.
8. Use `User.objects.create_user()` for passwords.
9. Keep a separate `COMMANDS.md` for each tutorial part.
