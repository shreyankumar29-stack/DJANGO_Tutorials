# Part 05 - Database & Migrations 📝

Detailed notes for **Part 05 of the Corey Schafer Django Tutorial Series**.

This part focuses on Django Models, Database Migrations, Django ORM, QuerySets, Django Shell, ForeignKey relationships, database records, and reverse relationships.

The purpose of these notes is to understand not only the code used in the tutorial, but also the reasoning behind each database operation and the debugging issues encountered while implementing it.

---

# 🎯 Learning Objectives

By the end of this part, I should understand:

- What a Django Model is.
- How Django Models connect to database tables.
- What migrations are.
- Difference between `makemigrations` and `migrate`.
- What Django ORM is.
- What a QuerySet is.
- How to query database records.
- How to create and save model objects.
- How ForeignKey relationships work.
- How Django's built-in `User` model relates to `Post`.
- Difference between `author` and `author_id`.
- How reverse relationships work.
- What `post_set` means.
- How to use the Django shell for database operations.
- How duplicate records can be accidentally created.
- How to debug common ORM and shell errors.

---

# 1. What is a Django Model?

A Django Model is a Python class that represents data stored in the database.

Example:

```python
class Post(models.Model):
    title = models.CharField(max_length=100)
    content = models.TextField()
    date_posted = models.DateTimeField(default=timezone.now)
    author = models.ForeignKey(User, on_delete=models.CASCADE)