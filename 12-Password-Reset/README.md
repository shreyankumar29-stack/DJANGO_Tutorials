# Django Tutorial – Video 11
## Pagination

### Overview
Video 11 adds pagination to the Django Blog and introduces a user-specific posts page.

### Concepts
- `ListView`
- `paginate_by`
- `page_obj`
- `paginator`
- `is_paginated`
- `get_queryset()`
- `get_object_or_404()`
- `self.kwargs`
- User-specific post URLs
- Previous/Next/First/Last pagination

### Main Post Pagination

```python
class PostListView(ListView):
    model = Post
    template_name = 'blog/home.html'
    context_object_name = 'posts'
    ordering = ['-date_posted']
    paginate_by = 5
```

`paginate_by = 5` displays a maximum of five posts per page.

### User-Specific Posts

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

This creates a page showing only posts written by the selected user.

### URL

```python
path(
    'user/<str:username>/',
    UserPostListView.as_view(),
    name='user-posts'
)
```

Example:

```text
/user/Shreyansh/
```

### Pagination Template Logic

```django
{% if is_paginated %}

    {% if page_obj.has_previous %}
        <a href="?page={{ page_obj.previous_page_number }}">
            Previous
        </a>
    {% endif %}

    {% for num in page_obj.paginator.page_range %}
        <a href="?page={{ num }}">{{ num }}</a>
    {% endfor %}

    {% if page_obj.has_next %}
        <a href="?page={{ page_obj.next_page_number }}">
            Next
        </a>
    {% endif %}

{% endif %}
```

### Important Variables

| Variable | Purpose |
|---|---|
| `paginate_by` | Objects per page |
| `page_obj` | Current page |
| `paginator` | Pagination information |
| `is_paginated` | Whether multiple pages exist |
| `has_previous()` | Checks previous page |
| `has_next()` | Checks next page |
| `previous_page_number()` | Gets previous page number |
| `next_page_number()` | Gets next page number |
| `page_range` | Available page numbers |

### Errors Encountered

#### NoReverseMatch

```text
Reverse for 'user-posts' not found.
```

Cause: the template used `user-posts`, but the URL pattern did not exist.

Fix:

```python
path(
    'user/<str:username>/',
    UserPostListView.as_view(),
    name='user-posts'
)
```

#### ImportError

```text
cannot import name 'UserPostListView' from 'blog.views'
```

Cause: `urls.py` imported `UserPostListView` before it was defined.

Fix: add `UserPostListView` to `blog/views.py`.

### Testing

- Home page loads
- Five posts per page
- Page navigation works
- Author name opens user-specific posts
- Only selected user's posts are displayed
- User-specific pagination works
- Invalid username returns 404
- Video 10 CRUD and authorization still work

### Project Structure

```text
11-Pagination/
└── django_project/
    ├── blog/
    │   ├── templates/blog/
    │   │   ├── base.html
    │   │   ├── home.html
    │   │   ├── post_detail.html
    │   │   ├── post_form.html
    │   │   ├── post_confirm_delete.html
    │   │   └── user_posts.html
    │   ├── models.py
    │   ├── urls.py
    │   └── views.py
    ├── users/
    ├── django_project/
    ├── media/
    ├── db.sqlite3
    └── manage.py
```

### Status
**Completed – Video 11**

### Reference
Django Pagination: https://docs.djangoproject.com/en/6.1/topics/pagination/
Django ListView: https://docs.djangoproject.com/en/6.1/ref/class-based-views/generic-display/
