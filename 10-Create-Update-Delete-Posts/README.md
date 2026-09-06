# Django Tutorial – Video 10
## Create, Update, and Delete Posts

### Overview
This part implements post CRUD using Django Class-Based Views (CBVs).

Covered:
- List posts
- View a single post
- Create posts
- Update posts
- Delete posts
- Restrict update/delete to the post owner
- Hide Update/Delete buttons for non-owners

Django provides generic class-based views for common model and form operations. citeturn0search0turn0search4

### Objectives
1. Class-Based Views
2. `ListView`
3. `DetailView`
4. `CreateView`
5. `UpdateView`
6. `DeleteView`
7. `LoginRequiredMixin`
8. `UserPassesTestMixin`
9. `form_valid()`
10. `test_func()`
11. `get_object()`
12. Ownership authorization
13. CRUD
14. Template conditions
15. `as_view()`

### CRUD Table

| Operation | View | Access |
|---|---|---|
| Read list | `PostListView` | Public |
| Read detail | `PostDetailView` | Public |
| Create | `PostCreateView` | Logged-in users |
| Update | `PostUpdateView` | Post owner |
| Delete | `PostDeleteView` | Post owner |

### Final `views.py`

```python
from django.views.generic import (
    ListView,
    DetailView,
    CreateView,
    UpdateView,
    DeleteView
)

from django.shortcuts import render
from django.contrib.auth.mixins import LoginRequiredMixin, UserPassesTestMixin

from .models import Post


def home(request):
    context = {
        'posts': Post.objects.all()
    }
    return render(request, 'blog/home.html', context)


class PostListView(ListView):
    model = Post
    template_name = 'blog/home.html'
    context_object_name = 'posts'
    ordering = ['-date_posted']


class PostDetailView(DetailView):
    model = Post


class PostCreateView(LoginRequiredMixin, CreateView):
    model = Post
    fields = ['title', 'content']

    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)


class PostUpdateView(LoginRequiredMixin, UserPassesTestMixin, UpdateView):
    model = Post
    fields = ['title', 'content']

    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)

    def test_func(self):
        post = self.get_object()
        return self.request.user == post.author


class PostDeleteView(LoginRequiredMixin, UserPassesTestMixin, DeleteView):
    model = Post
    success_url = '/'

    def test_func(self):
        post = self.get_object()
        return self.request.user == post.author


def about(request):
    return render(request, 'blog/about.html', {'title': 'About'})
```

### Why `UserPassesTestMixin` is not used for CreateView

A new post does not have an existing author to compare against. The author is assigned in `form_valid()`:

```python
form.instance.author = self.request.user
```

So Create uses only `LoginRequiredMixin`.

### Update Authorization

```python
def test_func(self):
    post = self.get_object()
    return self.request.user == post.author
```

If true, the owner can update. If false, Django rejects the request with `403 Forbidden`.

### Delete Authorization

Delete uses the same ownership check:

```python
class PostDeleteView(LoginRequiredMixin, UserPassesTestMixin, DeleteView):
    model = Post
    success_url = '/'

    def test_func(self):
        post = self.get_object()
        return self.request.user == post.author
```

Django's `DeleteView` displays a confirmation page and performs deletion through POST. citeturn0search5

### Final `post_detail.html`

```html
{% extends "blog/base.html" %}

{% block content %}
    <article class="media content-section">
        <img class="rounded-circle article-img"
             src="{{ object.author.profile.image.url }}">

        <div class="media-body">
            <div class="article-metadata">
                <a class="mr-2" href="#">{{ object.author }}</a>

                <small class="text-muted">
                    {{ object.date_posted|date:"F d, Y" }}
                </small>

                {% if user == object.author %}
                    <div>
                        <a class="btn btn-outline-info btn-sm mt-1 mb-1"
                           href="{% url 'post-update' object.id %}">
                            Update
                        </a>

                        <a class="btn btn-outline-danger btn-sm mt-1 mb-1"
                           href="{% url 'post-delete' object.id %}">
                            Delete
                        </a>
                    </div>
                {% endif %}
            </div>

            <h2 class="article-title">{{ object.title }}</h2>
            <p class="article-content">{{ object.content }}</p>
        </div>
    </article>
{% endblock content %}
```

### UI vs Backend Security

The template:

```django
{% if user == object.author %}
```

only hides the buttons.

The actual security comes from `UserPassesTestMixin` and `test_func()`.

Therefore, if another user manually enters the update URL, the backend still returns `403 Forbidden`.

### Error Encountered

Error:

```text
NotImplementedError:
PostCreateView is missing the implementation of the test_func() method.
```

Cause:

```python
class PostCreateView(LoginRequiredMixin, UserPassesTestMixin, CreateView):
```

Fix:

```python
class PostCreateView(LoginRequiredMixin, CreateView):
```

`UserPassesTestMixin` remains on UpdateView and DeleteView.

### Testing

Owner:
```text
User = Shreyansh
Post author = Shreyansh
→ Update/Delete allowed
```

Other user:
```text
User = User B
Post author = Shreyansh
→ Buttons hidden
→ Direct update/delete → 403 Forbidden
```

### Project Structure

```text
10-Create-Update-Delete-Posts/
└── django_project/
    ├── blog/
    │   ├── templates/blog/
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
**Completed – Video 10**

### References
- Django generic editing views: urlDjango Class-Based Generic Editing Viewshttps://docs.djangoproject.com/en/6.1/topics/class-based-views/generic-editing/
- Django class-based view mixins: urlDjango Class-Based View Mixinshttps://docs.djangoproject.com/en/6.1/topics/class-based-views/mixins/
