# Part 05 - Database & Migrations 🛠️

Complete command reference for **Part 05 - Database and Migrations** from the Corey Schafer Django Tutorial Series.

This file contains the commands and Django shell operations used while working with:

- Django Models
- Migrations
- Django ORM
- QuerySets
- Django Shell
- Users
- Posts
- ForeignKey Relationships
- Database Records
- Git & GitHub

---

# 📁 Project Location

Run Django `manage.py` commands from the directory containing:

```text
manage.py
```

Example:

```text
05-Database-And-Migrations/
└── django_project/
    ├── manage.py
    ├── django_project/
    └── blog/
```

---

# 🐍 1. Virtual Environment

## Activate Virtual Environment

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

After activation:

```text
(.venv)
```

should appear in the terminal.

---

## Activate in Command Prompt

```cmd
.venv\Scripts\activate
```

---

## Deactivate Virtual Environment

```powershell
deactivate
```

---

# 🐍 2. Python & pip

## Check Python Version

```powershell
python --version
```

## Check pip Version

```powershell
pip --version
```

---

# 📦 3. Django

## Install Django

```powershell
pip install django
```

## Check Django Version

```powershell
python -m django --version
```

or:

```powershell
django-admin --version
```

## Show Django Package Information

```powershell
pip show django
```

---

# 🚀 4. Start Development Server

```powershell
python manage.py runserver
```

Default URL:

```text
http://127.0.0.1:8000/
```

---

# 🔌 5. Run Server on Another Port

```powershell
python manage.py runserver 8001
```

Then:

```text
http://127.0.0.1:8001/
```

---

# 🛑 6. Stop Development Server

```text
CTRL + C
```

---

# ✅ 7. Django System Check

```powershell
python manage.py check
```

This checks the project for common configuration errors.

---

# 🗄️ 8. Migrations

## Create Migration Files

After changing models:

```powershell
python manage.py makemigrations
```

This creates migration files based on changes in `models.py`.

---

## Apply Migrations

```powershell
python manage.py migrate
```

This applies migration files to the database.

---

## Show Migration Status

```powershell
python manage.py showmigrations
```

---

# 🐚 9. Start Django Shell

```powershell
python manage.py shell
```

The Django shell gives access to the project's models and ORM.

Example prompt:

```text
>>>
```

---

# 📥 10. Import the Post Model

Inside Django shell:

```python
from blog.models import Post
```

---

# 📥 11. Import Django User Model

```python
from django.contrib.auth.models import User
```

---

# 👥 12. Show All Users

```python
User.objects.all()
```

Example:

```text
<QuerySet [<User: Shreyansh>]>
```

If no users exist:

```text
<QuerySet []>
```

An empty QuerySet means there are currently no matching records.

---

# 👤 13. Get a Specific User

```python
user = User.objects.get(username='Shreyansh')
```

Replace `Shreyansh` with the actual username in the database.

---

# 🔎 14. Display the User Object

```python
user
```

Example:

```text
<User: Shreyansh>
```

---

# 🆔 15. Get User ID

```python
user.id
```

Example:

```text
1
```

---

# 👤 16. Get User Username

```python
user.username
```

---

# 📧 17. Get User Email

```python
user.email
```

---

# 📝 18. Show All Blog Posts

```python
Post.objects.all()
```

If no posts exist:

```text
<QuerySet []>
```

---

# ➕ 19. Create First Post

```python
post_1 = Post(
    title='Blog 1',
    content='First Post!',
    author=user
)
```

Here:

```text
author=user
```

is important because `author` is a ForeignKey to the `User` model.

---

# 💾 20. Save First Post

```python
post_1.save()
```

This saves the post to the database.

---

# 🔎 21. Check Posts Again

```python
Post.objects.all()
```

Example:

```text
<QuerySet [<Post: Blog 1>]>
```

---

# ➕ 22. Create Second Post

```python
post_2 = Post(
    title='Blog 2',
    content='Second Blog Content!',
    author=user
)
```

---

# 💾 23. Save Second Post

```python
post_2.save()
```

---

# 🔎 24. Check All Posts

```python
Post.objects.all()
```

Example:

```text
<QuerySet [<Post: Blog 1>, <Post: Blog 2>]>
```

---

# 🔗 25. ForeignKey Using the User Object

Recommended form:

```python
post_2 = Post(
    title='Blog 2',
    content='Second Blog Content!',
    author=user
)
```

Here:

```text
author → User instance
```

---

# 🔗 26. ForeignKey Using the User ID

You can also use:

```python
post_2 = Post(
    title='Blog 2',
    content='Second Blog Content!',
    author_id=user.id
)
```

Here:

```text
author_id → Numeric User ID
```

---

# ❌ 27. Incorrect ForeignKey Assignment

Do not use:

```python
author='user'
```

because a string is not a `User` instance.

Correct:

```python
author=user
```

---

# ❌ 28. Incorrect `author_id`

Do not use:

```python
author_id=user
```

because `author_id` expects the numeric primary key.

Correct:

```python
author_id=user.id
```

---

# 🔎 29. Filter Posts by Title

```python
Post.objects.filter(title='Blog 1')
```

---

# 🔎 30. Filter Posts by Author

```python
Post.objects.filter(author=user)
```

---

# 🔎 31. Filter Posts by Author ID

```python
Post.objects.filter(author_id=user.id)
```

---

# 🎯 32. Get One Post by ID

```python
Post.objects.get(id=1)
```

Replace `1` with the required Post ID.

---

# 🎯 33. Get Post by Title

```python
Post.objects.get(title='Blog 1')
```

Use `get()` when one matching object is expected.

---

# 🥇 34. Get First Post

```python
Post.objects.all().first()
```

---

# 🥉 35. Get Last Post

```python
Post.objects.all().last()
```

---

# 🔢 36. Count Posts

```python
Post.objects.all().count()
```

---

# 🧪 37. Create a Post with `objects.create()`

Django ORM can create and save an object in one operation:

```python
Post.objects.create(
    title='Blog 3',
    content='Third Post!',
    author=user
)
```

This avoids separately calling:

```python
post.save()
```

---

# 🚪 38. Exit Django Shell

```python
exit()
```

On Windows you can also use:

```text
CTRL + Z
```

then press Enter.

---

# 👑 39. Create Superuser

If Admin access is required:

```powershell
python manage.py createsuperuser
```

Then open:

```text
http://127.0.0.1:8000/admin/
```

---

# 🌐 40. Important URLs

## Home

```text
http://127.0.0.1:8000/
```

## About

```text
http://127.0.0.1:8000/about/
```

## Admin

```text
http://127.0.0.1:8000/admin/
```

---

# 🔍 41. Debugging an Empty QuerySet

If:

```python
User.objects.all()
```

returns:

```text
<QuerySet []>
```

it means there are no User records matching the query.

Similarly:

```python
Post.objects.all()
```

returning:

```text
<QuerySet []>
```

means there are no Post records.

---

# 🐛 42. Debugging ForeignKey Errors

If you see:

```text
ValueError:
"Post.author" must be a "User" instance.
```

check whether you accidentally used:

```python
author='user'
```

Use:

```python
author=user
```

instead.

For an ID:

```python
author_id=user.id
```

---

# 🐛 43. Debugging `NameError: post_1`

If Post creation fails:

```python
post_1 = Post(...)
```

then this may not create the variable.

Running:

```python
post_1.save()
```

after the failed assignment can produce:

```text
NameError: name 'post_1' is not defined
```

Fix the original creation error first, then recreate the object.

---

# 🐛 44. Debugging `NameError: user_id`

If this is used:

```python
author_id=user_id
```

without defining `user_id`, Python raises:

```text
NameError: name 'user_id' is not defined
```

Define it first:

```python
user_id = user.id
```

or use:

```python
author_id=user.id
```

directly.

---

# 🗃️ 45. Database Inspection Workflow

A simple workflow for Part 05:

```text
python manage.py shell
        ↓
from blog.models import Post
        ↓
from django.contrib.auth.models import User
        ↓
User.objects.all()
        ↓
user = User.objects.get(...)
        ↓
Post.objects.all()
        ↓
post = Post(...)
        ↓
post.save()
        ↓
Post.objects.all()
```

---

# 🔄 46. Migration Workflow

Whenever the model changes:

```text
Edit models.py
     ↓
python manage.py makemigrations
     ↓
Migration file
     ↓
python manage.py migrate
     ↓
Database updated
```

---

# 📋 47. Quick Django Command Reference

| Command | Purpose |
|---|---|
| `python manage.py runserver` | Start development server |
| `python manage.py check` | Check Django configuration |
| `python manage.py makemigrations` | Create migration files |
| `python manage.py migrate` | Apply migrations |
| `python manage.py showmigrations` | Show migration status |
| `python manage.py shell` | Open Django shell |
| `python manage.py createsuperuser` | Create admin user |
| `python manage.py startapp blog` | Create Blog app |
| `python -m django --version` | Check Django version |
| `pip show django` | Show Django package |

---

# 📋 48. Quick ORM Reference

| Query | Purpose |
|---|---|
| `User.objects.all()` | Get all users |
| `User.objects.get(username='...')` | Get a specific user |
| `Post.objects.all()` | Get all posts |
| `Post.objects.filter(...)` | Filter posts |
| `Post.objects.get(...)` | Get one post |
| `Post.objects.create(...)` | Create and save a post |
| `post.save()` | Save a model instance |
| `post.id` | Get object ID |
| `Post.objects.all().first()` | First post |
| `Post.objects.all().last()` | Last post |
| `Post.objects.all().count()` | Number of posts |

---

# 🗂️ 49. Quick ForeignKey Reference

```python
author=user
```

✅ `User` model instance.

```python
author_id=user.id
```

✅ Numeric primary key.

```python
author='user'
```

❌ String.

```python
author_id=user
```

❌ User object instead of numeric ID.

```python
author_id=user_id
```

❌ Unless `user_id` has been defined.

---

# 📦 50. Save Dependencies

Show installed packages:

```powershell
pip freeze
```

Save dependencies:

```powershell
pip freeze > requirements.txt
```

Install dependencies later:

```powershell
pip install -r requirements.txt
```

---

# 🔧 51. Git & GitHub

## Check Git Status

```powershell
git status
```

## Add Part 05

```powershell
git add "05-Database-And-Migrations"
```

## Commit

```powershell
git commit -m "Add Django Part 05 database and migrations"
```

## Push

```powershell
git push origin main
```

## View Recent Commits

```powershell
git log --oneline -5
```

---

# ✅ 52. Part 05 Checklist

## Environment

- [x] Activate `.venv`
- [x] Check Python
- [x] Check Django

## Database

- [x] Run `makemigrations`
- [x] Run `migrate`
- [x] Check migration status

## Django Shell

- [x] Start shell
- [x] Import `Post`
- [x] Import `User`
- [x] Query users
- [x] Get a specific user
- [x] Query posts
- [x] Create posts
- [x] Save posts
- [x] Filter QuerySets
- [x] Retrieve objects
- [x] Count objects

## Relationships

- [x] Understand `author`
- [x] Understand `author_id`
- [x] Use `User` instance
- [x] Use `user.id`

## Debugging

- [x] Empty QuerySet
- [x] ForeignKey assignment error
- [x] `post_1` NameError
- [x] `user_id` NameError

## GitHub

- [x] Check status
- [x] Add Part 05
- [x] Commit
- [x] Push

---

# 🎯 Part 05 Complete

The commands and Django shell operations documented here cover the database, migration, ORM, QuerySet, model creation, and ForeignKey workflow used while following Part 05 of the Corey Schafer Django Tutorial Series.
