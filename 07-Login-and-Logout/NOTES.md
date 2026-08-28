# Notes – Video 7: Login and Logout

## Authentication

Django provides a built-in authentication system.

Template check:

```django
{% if user.is_authenticated %}
```

## Registration

`UserRegisterForm` creates a new user.

After registration:

```python
return redirect('login')
```

## Login

Use Django's built-in `LoginView`:

```python
auth_views.LoginView.as_view(
    template_name='users/login.html'
)
```

Settings:

```python
LOGIN_URL = 'login'
LOGIN_REDIRECT_URL = 'blog-home'
```

## Logout

A direct logout link such as:

```html
<a href="{% url 'logout' %}">Logout</a>
```

can cause HTTP 405 with newer Django versions.

Use a POST form:

```html
<form action="{% url 'logout' %}" method="POST">
    {% csrf_token %}
    <button type="submit">Logout</button>
</form>
```

## Profile

Protect the profile page with:

```python
@login_required
def profile(request):
    return render(request, 'users/profile.html')
```

## Crispy Forms

Packages:

```text
django-crispy-forms
crispy-bootstrap4
```

Settings:

```python
CRISPY_ALLOWED_TEMPLATE_PACKS = "bootstrap4"
CRISPY_TEMPLATE_PACK = "bootstrap4"
```

## Pillow

`Pillow` is required for:

```python
models.ImageField
```

Install:

```powershell
python -m pip install Pillow
```

## Media Files

```python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

`MEDIA_ROOT` stores uploaded files and `MEDIA_URL` defines their URL prefix.

## Common Errors

### `TemplateDoesNotExist: bootstrap4/uni_form.html`

Install Bootstrap 4 support:

```powershell
python -m pip install crispy-bootstrap4
```

and add:

```python
'crispy_bootstrap4',
```

to `INSTALLED_APPS`.

### `HTTP 405 Method Not Allowed` on Logout

Logout was requested with GET.

Use a POST form and a suitable logout view.

### `NoReverseMatch: Reverse for 'profile' not found`

The template referenced `profile` before its URL existed.

Make sure the profile URL/view exists before using:

```django
{% url 'profile' %}
```

### `AttributeError: module 'users.views' has no attribute 'profile'`

`urls.py` referenced `user_views.profile` while the view was missing.

Create the view or remove the URL until the feature is implemented.

## Useful Commands

```powershell
python manage.py check
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
python -m pip freeze > requirements.txt
```


