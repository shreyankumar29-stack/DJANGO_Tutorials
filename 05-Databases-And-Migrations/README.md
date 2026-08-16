# Part 05 - Database & Migrations 🚀

A comprehensive Django learning project created while following the **Corey Schafer Django Tutorial Series**.

This part focuses on **Django Models, Database Migrations, Django ORM, QuerySets, Django Shell, and ForeignKey Relationships** while continuing the Django Blog project.

This repository serves as my personal **Django study and revision guide**. It contains the code written during the tutorial, along with detailed documentation, notes, debugging solutions, and modern Django compatibility updates.

The primary purpose of this project is **learning and revision**, not production deployment.

---

# 📚 Repository Purpose

This part was created to:

* Understand Django Models.
* Understand database migrations.
* Learn how Django ORM works.
* Work with QuerySets.
* Create, save, and retrieve database records.
* Understand ForeignKey relationships.
* Work with Django's built-in `User` model.
* Practice database operations through the Django shell.
* Record debugging solutions and common errors.

---

# 📖 Topics Covered

### Django Models

* Django Models
* Model Fields
* Model Instances
* Model Relationships
* ForeignKey

### Database & Migrations

* Database Migrations
* `makemigrations`
* `migrate`
* Database Tables
* SQLite Database

### Django ORM

* QuerySets
* `objects.all()`
* `objects.get()`
* Creating Model Objects
* Saving Objects
* Retrieving Records

### Django Shell

* Starting Django Shell
* Importing Models
* Querying Users
* Querying Blog Posts
* Creating Objects
* Saving Objects

### Relationships

* `User` and `Post`
* ForeignKey Relationships
* Model Instance vs ID
* `author`
* `author_id`

### Debugging

* Empty QuerySets
* ForeignKey Assignment Errors
* Undefined Variables
* `User` Instance vs Numeric ID

---

# 📝 What I Learned

* How Django Models represent database tables.
* How migrations synchronize model changes with the database.
* How to use Django ORM instead of writing raw SQL for common database operations.
* What a QuerySet is.
* How `objects.all()` works.
* How `objects.get()` retrieves a specific record.
* How to create and save model instances.
* How ForeignKey relationships work.
* Why a ForeignKey field can accept a model instance.
* The difference between `author` and `author_id`.
* How to work with Django's built-in `User` model through the Django shell.

---

# 🛠️ Tech Stack

* Python 3
* Django
* SQLite
* Django ORM
* Django Shell
* HTML5
* CSS3
* Bootstrap
* VS Code
* Git
* GitHub

---

# 📂 Repository Structure

```text
05-Database-And-Migrations/

├── django_project/
│   │
│   ├── manage.py
│   │
│   ├── django_project/
│   │   ├── __init__.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   ├── asgi.py
│   │   └── wsgi.py
│   │
│   └── blog/
│       │
│       ├── migrations/
│       ├── static/
│       ├── templates/
│       ├── __init__.py
│       ├── admin.py
│       ├── apps.py
│       ├── models.py
│       ├── tests.py
│       ├── urls.py
│       └── views.py
│
├── README.md
├── NOTES.md
└── COMMANDS.md
```

---

# 🗄️ Database & Migrations

Django uses migrations to keep the database schema synchronized with the models.

Typical workflow:

```text
Model Changes
     ↓
makemigrations
     ↓
Migration Files
     ↓
migrate
     ↓
Database
```

### Create Migration Files

```bash
python manage.py makemigrations
```

### Apply Migrations

```bash
python manage.py migrate
```

---

# 🧠 Django ORM

Django ORM allows Python code to work with database records through model classes.

For example:

```python
User.objects.all()
```

returns a QuerySet containing User records.

A specific User can be retrieved using:

```python
User.objects.get(username='Shreyansh')
```

---

# 🔎 QuerySets

A QuerySet represents a collection of database records returned by the Django ORM.

Example:

```python
User.objects.all()
```

Possible result:

```text
<QuerySet [<User: Shreyansh>]>
```

If the database contains no matching records:

```text
<QuerySet []>
```

An empty QuerySet does **not** mean the ORM is broken. It means there are currently no matching records in the database.

---

# 🔗 ForeignKey Relationships

A Blog `Post` can have an author related to Django's built-in `User` model.

Conceptually:

```text
User
  │
  └── Post
```

Example:

```python
user = User.objects.get(username='Shreyansh')

post = Post(
    title='Blog 1',
    content='First Post!',
    author=user
)
```

---

# ⚠️ `author` vs `author_id`

For a ForeignKey field:

```python
author=user
```

is valid because `author` expects a `User` instance.

The underlying ID can be assigned using:

```python
author_id=user.id
```

Examples:

```python
author=user          # ✅ User instance
author_id=user.id   # ✅ Numeric ID

author='user'       # ❌ String
author_id=user      # ❌ User object
author_id=user_id   # ❌ Unless user_id was defined
```

---

# 🐛 Debugging Experience

### Empty QuerySet

```text
<QuerySet []>
```

This means no matching records currently exist in the database.

---

### ForeignKey Assignment Error

Error:

```text
ValueError:
"Post.author" must be a "User" instance.
```

Cause:

```python
author='user'
```

Solution:

```python
author=user
```

---

### `post_1` NameError

If creating the `Post` object fails, the variable may never be created.

Then:

```python
post_1.save()
```

can produce:

```text
NameError: name 'post_1' is not defined
```

---

### `user_id` NameError

Using:

```python
author_id=user_id
```

without defining `user_id` produces:

```text
NameError: name 'user_id' is not defined
```

Use:

```python
user_id = user.id
```

or directly:

```python
author_id=user.id
```

---

# 🎯 Learning Goals

The purpose of this part is to:

* Understand the connection between Models and the database.
* Learn the migration workflow.
* Understand Django ORM basics.
* Work with QuerySets.
* Create and save database records.
* Understand ForeignKey relationships.
* Use the Django shell for database operations.
* Build the foundation for database-backed Blog posts.

---

# ⭐ Repository Highlights

* Django Models
* Database Migrations
* Django ORM
* QuerySets
* Django Shell
* ForeignKey Relationships
* Built-in User Model
* Database Record Creation
* Database Debugging
* Detailed Documentation
* Modern Django Compatibility

---

# 📖 Documentation

This part contains:

### README.md

Provides:

* Part overview
* Topics covered
* Learning goals
* Project structure
* Tech stack
* Key takeaways

### NOTES.md

Contains:

* Detailed concepts
* Django ORM explanations
* QuerySet explanations
* ForeignKey relationships
* Django Shell examples
* Debugging solutions
* Interview questions
* Revision material

### COMMANDS.md

Contains:

* Django management commands
* Migration commands
* Shell commands
* Database-related commands
* Git commands
* Quick command reference

---

# ⚠️ Note

This project is intended for **learning and revision purposes**.

The code and database operations in this part are based on the Corey Schafer Django Tutorial Series.

The original tutorial uses an older Django version, so code is updated where necessary to remain compatible with the modern Django environment.

---

# 📚 Learning Resource

**Tutorial Series:**

Corey Schafer – Django Tutorial Series (YouTube)

---

# 🚀 Future Plans

Continue developing the Django Blog application by:

* Creating database-backed Blog posts.
* Using Django ORM more extensively.
* Building CRUD functionality.
* Adding authentication features.
* Connecting users with posts.
* Managing data through Django Admin.
* Building a complete original Django project after finishing the core tutorial series.

---

Happy Learning! 🚀
