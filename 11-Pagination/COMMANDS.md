# Video 11 Commands – Pagination

## Project Directory

```powershell
cd "C:\Users\Shreyansh kumar\Documents\DJANGO_Tutorials"
```

## Activate Virtual Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

## Enter Video 11

```powershell
cd "11-Pagination\django_project"
```

## Check Django Version

```powershell
python -m django --version
```

## Check Project

```powershell
python manage.py check
```

Expected:

```text
System check identified no issues (0 silenced).
```

## Run Server

```powershell
python manage.py runserver
```

## Pagination URLs

Home:

```text
http://127.0.0.1:8000/
```

Page 2:

```text
http://127.0.0.1:8000/?page=2
```

User posts:

```text
http://127.0.0.1:8000/user/Shreyansh/
```

User page 2:

```text
http://127.0.0.1:8000/user/Shreyansh/?page=2
```

Replace `Shreyansh` with the actual username.

## Django Shell

```powershell
python manage.py shell
```

```python
from blog.models import Post
Post.objects.all()
```

Count posts:

```python
Post.objects.count()
```

Print posts:

```python
for post in Post.objects.all():
    print(post.id, post.title, post.author)
```

Exit:

```python
exit()
```

## Testing Pagination

With:

```python
paginate_by = 5
```

```text
5 posts  → 1 page
6 posts  → 2 pages
10 posts → 2 pages
11 posts → 3 pages
```

## Git

```powershell
git status
git add .
git commit -m "Complete Video 11 pagination"
git push
```

## Optional Requirements

```powershell
python -m pip freeze > requirements.txt
```

## Important

No migration is normally required for Video 11 because the changes are in views, URLs, and templates.

Do not delete:

```text
db.sqlite3
```

## Final Verification

```powershell
python manage.py check
python manage.py runserver
```

Then test:

1. Home page
2. Page 2
3. Page 3 if enough posts exist
4. Author name
5. User-specific posts page
6. User-specific pagination
7. Invalid username → 404
8. Create post
9. Update own post
10. Delete own post
