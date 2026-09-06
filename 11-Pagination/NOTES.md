# Video 11 Notes – Pagination

## 1. Pagination

Pagination divides a large list into smaller pages.

Example:

```text
20 posts
↓
paginate_by = 5
↓
4 pages
```

## 2. paginate_by

```python
paginate_by = 5
```

Controls the maximum number of objects shown on one page.

## 3. page_obj

Represents the current page.

```django
{{ page_obj.number }}
```

Useful methods:

```python
page_obj.has_previous()
page_obj.has_next()
page_obj.previous_page_number()
page_obj.next_page_number()
```

## 4. paginator

Useful values:

```django
{{ page_obj.paginator.count }}
{{ page_obj.paginator.num_pages }}
{{ page_obj.paginator.page_range }}
```

## 5. is_paginated

```django
{% if is_paginated %}
```

Checks whether pagination is active.

## 6. Previous

```django
{% if page_obj.has_previous %}
    <a href="?page={{ page_obj.previous_page_number }}">
        Previous
    </a>
{% endif %}
```

## 7. Next

```django
{% if page_obj.has_next %}
    <a href="?page={{ page_obj.next_page_number }}">
        Next
    </a>
{% endif %}
```

## 8. UserPostListView

```python
class UserPostListView(ListView):
    model = Post
    template_name = 'blog/user_posts.html'
    context_object_name = 'posts'
    paginate_by = 5

    def get_queryset(self):
        user = get_object_or_404(
            User,
            username=self.kwargs.get('username')
        )

        return Post.objects.filter(
            author=user
        ).order_by('-date_posted')
```

## 9. get_queryset()

`get_queryset()` allows us to dynamically filter the objects returned by a `ListView`.

```python
Post.objects.filter(author=user)
```

returns only posts written by that user.

## 10. self.kwargs

For:

```python
path('user/<str:username>/', ...)
```

the username is available through:

```python
self.kwargs.get('username')
```

## 11. get_object_or_404()

```python
get_object_or_404(User, username=...)
```

Returns the user if found; otherwise Django returns a 404 response.

## 12. URL Name

```python
name='user-posts'
```

allows:

```django
{% url 'user-posts' post.author.username %}
```

## 13. Common Errors

### NoReverseMatch

```text
Reverse for 'user-posts' not found.
```

Fix the missing URL pattern.

### ImportError

```text
cannot import name 'UserPostListView'
```

Define the class in `views.py` before importing it in `urls.py`.

## 14. Core Flow

```text
URL
 ↓
ListView
 ↓
QuerySet
 ↓
paginate_by
 ↓
page_obj
 ↓
Template
 ↓
Pagination controls
```

User-specific:

```text
/user/Shreyansh/
        ↓
UserPostListView
        ↓
self.kwargs['username']
        ↓
get_object_or_404()
        ↓
Post.objects.filter(author=user)
        ↓
paginate_by = 5
        ↓
user_posts.html
```

## 15. Main Takeaways

```text
paginate_by       → objects per page
page_obj          → current page
paginator         → pagination information
get_queryset()    → customize/filter QuerySet
self.kwargs       → URL parameters
get_object_or_404 → object or 404
```
