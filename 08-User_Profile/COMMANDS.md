# Commands -- Video 8: User Profile & Picture

## Activate Virtual Environment

``` powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
.\.venv\Scripts\Activate.ps1
```

## Go to Project Directory

``` powershell
cd "08-User_Profile\django_project"
```

## Install Pillow

``` powershell
python -m pip install Pillow
```

## Check Django Project

``` powershell
python manage.py check
```

## Create Migrations

After changing models:

``` powershell
python manage.py makemigrations
```

For the users app specifically:

``` powershell
python manage.py makemigrations users
```

## Apply Migrations

``` powershell
python manage.py migrate
```

## Open Django Shell

``` powershell
python manage.py shell
```

## Check Users

``` python
from django.contrib.auth.models import User
User.objects.all()
```

## Check Profiles

``` python
from users.models import Profile
Profile.objects.all()
```

## Check a User's Profile

``` python
Profile.objects.get(user__username='NewUser')
```

## Check Profile Image Path

``` python
Profile.objects.get(user__username='NewUser').image.name
```

Expected:

``` text
'profile_pics/default.jpg'
```

## Exit Django Shell

``` python
exit()
```

## Run Development Server

``` powershell
python manage.py runserver
```

Open:

``` text
http://127.0.0.1:8000/
```

## Open Profile Page

``` text
http://127.0.0.1:8000/profile/
```

## Open Django Admin

``` text
http://127.0.0.1:8000/admin/
```

## Update Requirements

``` powershell
python -m pip freeze > requirements.txt
```

## Git Commands

``` powershell
git status
git add .
git commit -m "Complete Video 8 user profile and picture"
git push
```
