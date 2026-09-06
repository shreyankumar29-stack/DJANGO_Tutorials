# Video 10 Notes – Create, Update, and Delete Posts

## 1. Class-Based Views

Django generic class-based views reduce repeated code.

Main views:

```python
ListView
DetailView
CreateView
UpdateView
DeleteView
```

## 2. ListView

```python
class PostListView(ListView):
    model = Post
    template_name = 'blog/home.html'
    context_object_name = 'posts'
    ordering = ['-date_posted']
```

## 3. DetailView

```python
class PostDetailView(DetailView):
    model = Post
```

The current object is available as:

```django
{{ object }}
```

## 4. CreateView

```python
class PostCreateView(LoginRequiredMixin, CreateView):
    model = Post
    fields = ['title', 'content']

    def form_valid(self, form):
        form.instance.author = self.request.user
        return super().form_valid(form)
```

`form_valid()` assigns the logged-in user as author. Django documents this pattern for attaching `request.user` during creation. citeturn0search2

## 5. LoginRequiredMixin

```python
LoginRequiredMixin
```

Requires authentication before accessing the view.

## 6. UserPassesTestMixin

Used when access depends on a custom test.

```python
def test_func(self):
    post = self.get_object()
    return self.request.user == post.author
```

Result:

```text
True  → allowed
False → 403 Forbidden
```

## 7. UpdateView

```python
class PostUpdateView(LoginRequiredMixin, UserPassesTestMixin, UpdateView):
```

Only the post owner should be able to update.

## 8. DeleteView

```python
class PostDeleteView(LoginRequiredMixin, UserPassesTestMixin, DeleteView):
```

Only the post owner should be able to delete.

## 9. Why CreateView Does Not Use UserPassesTestMixin

Wrong:

```python
class PostCreateView(LoginRequiredMixin, UserPassesTestMixin, CreateView):
```

Correct:

```python
class PostCreateView(LoginRequiredMixin, CreateView):
```

A new object has no existing author yet.

## 10. Template Authorization

```django
{% if user == object.author %}
    Update
    Delete
{% endif %}
```

This hides controls from non-owners.

## 11. Backend Authorization

Hiding buttons is not enough.

The view also checks:

```python
return self.request.user == post.author
```

This prevents manual URL access.

## 12. Why Corey Gets 403

If:

```text
request.user != post.author
```

then:

```python
test_func()
```

returns `False`.

The request is rejected with:

```text
403 Forbidden
```

## 13. Error and Fix

Error:

```text
PostCreateView is missing the implementation of the test_func() method.
```

Cause:

`UserPassesTestMixin` was incorrectly added to CreateView.

Fix:

```python
class PostCreateView(LoginRequiredMixin, CreateView):
```

## 14. Core Pattern

```text
Create  → LoginRequiredMixin
Update  → LoginRequiredMixin + UserPassesTestMixin
Delete  → LoginRequiredMixin + UserPassesTestMixin
```

## 15. Main Takeaways

- CBVs reduce boilerplate.
- `form_valid()` can assign the current user.
- `LoginRequiredMixin` checks authentication.
- `UserPassesTestMixin` checks custom authorization.
- `test_func()` checks ownership.
- Template checks improve UI.
- Backend checks provide actual authorization.
