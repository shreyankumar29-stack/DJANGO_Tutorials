# Commands -- Video 9: Update User Profile

## Activate Virtual Environment

``` powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
.\.venv\Scripts\Activate.ps1
```

## Go to Video 9 Project

``` powershell
cd "09-Update-User-Profile\django_project"
```

## Check Project

``` powershell
python manage.py check
```

## Install Pillow

``` powershell
python -m pip install Pillow
```

## Create Migrations

If models were changed:

``` powershell
python manage.py makemigrations
```

For users specifically:

``` powershell
python manage.py makemigrations users
```

## Apply Migrations

``` powershell
python manage.py migrate
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

## Open Django Shell

``` powershell
python manage.py shell
```

## Check Profiles

``` python
from users.models import Profile
Profile.objects.all()
```

## Check a User's Image

``` python
Profile.objects.get(user__username='NewUser').image.name
```

## Exit Shell

``` python
exit()
```

## Update Requirements

``` powershell
python -m pip freeze > requirements.txt
```

## Git Commands

``` powershell
git status
git add .
git commit -m "Complete Video 9 update user profile"
git push
```
