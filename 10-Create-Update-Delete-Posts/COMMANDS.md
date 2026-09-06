# Video 10 Commands – Create, Update, and Delete Posts

## 1. Project Directory

```powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
```

## 2. Activate Virtual Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

## 3. Enter Video 10

```powershell
cd "10-Create-Update-Delete-Posts\django_project"
```

## 4. Check Project

```powershell
python manage.py check
```

## 5. Migrations

Only if required:

```powershell
python manage.py makemigrations
python manage.py migrate
```

View changes in migrations:

```powershell
python manage.py showmigrations
```

## 6. Run Server

```powershell
python manage.py runserver
```

Open:

```text
http://127.0.0.1:8000/
```

## 7. Useful URLs

```text
/
```

```text
/post/new/
```

```text
/post/1/
```

```text
/post/1/update/
```

```text
/post/1/delete/
```

## 8. Django Shell

```powershell
python manage.py shell
```

```python
from blog.models import Post
Post.objects.all()
```

Check authors:

```python
for post in Post.objects.all():
    print(post.id, post.title, post.author)
```

Exit:

```python
exit()
```

## 9. Ownership Test

Example:

```text
Post 1 → Shreyansh
Post 2 → testUser
```

Login as Shreyansh.

```text
/post/1/update/
```

Expected: allowed.

Then:

```text
/post/2/update/
```

Expected:

```text
403 Forbidden
```

## 10. Git

```powershell
git status
git add .
git commit -m "Complete Video 10 create update delete posts"
git push
```

## 11. Requirements

```powershell
python -m pip freeze > requirements.txt
```

## 12. Important

Do not delete:

```text
db.sqlite3
```

Do not reset migrations unnecessarily.

## 13. Final Test Checklist

1. Login.
2. Create a post.
3. Open the post.
4. Update your own post.
5. Delete your own post.
6. Login as another user.
7. Open the first user's post.
8. Confirm Update/Delete buttons are hidden.
9. Manually open the update URL.
10. Confirm `403 Forbidden`.
