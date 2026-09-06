# Django Tutorial -- Video 12 Commands

## 1. Repository Root

``` powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
```

## 2. Activate Virtual Environment

``` powershell
.\.venv\Scripts\Activate.ps1
```

## 3. Part 12 Directory

``` powershell
cd "12-Password-Reset\django_project"
```

## 4. Django Version

``` powershell
python -m django --version
```

## 5. Install dotenv

``` powershell
python -m pip install python-dotenv
```

## 6. Project Check

``` powershell
python manage.py check
```

## 7. Run Server

``` powershell
python manage.py runserver
```

## 8. Password Reset Page

``` text
http://127.0.0.1:8000/password-reset/
```

## 9. Check Email Configuration

``` powershell
python manage.py shell
```

``` python
from django.conf import settings
print(settings.EMAIL_HOST_USER)
print(bool(settings.EMAIL_HOST_PASSWORD))
```

Exit:

``` python
exit()
```

## 10. Check Registered User Emails

``` powershell
python manage.py shell
```

``` python
from django.contrib.auth.models import User

for user in User.objects.all():
    print(user.username, user.email)
```

Exit:

``` python
exit()
```

## 11. Manually Reset a Password

``` powershell
python manage.py changepassword Shreyansh
```

## 12. Git Commands

From the repository root:

``` powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
git status
git add .
git commit -m "Complete Video 12 password reset"
git push
```

## 13. Important

Do not commit:

``` text
.env
```

`.gitignore` must contain:

``` gitignore
.env
```

Never put the Gmail App Password directly into tracked source files.
