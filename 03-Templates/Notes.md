# Part 03 - Templates 📝

This document contains detailed notes for **Part 03 - Templates** of the Corey Schafer Django Tutorial Series.

The main focus of this part is understanding Django's **Template System, Template Inheritance, Context Data, Static Files, Bootstrap, and the basic Blog layout**.

---

# 🎯 Learning Objectives

By completing this part, I learned:

- What Django Templates are.
- How Django renders an HTML template.
- How a View passes data to a Template.
- What a Context Dictionary is.
- How Django Template Language works.
- How `{% for %}` loops work.
- What Template Inheritance is.
- How `{% extends %}` works.
- How `{% block %}` works.
- How Static Files work.
- How to connect CSS with Django.
- How Bootstrap is integrated into a Django project.
- How to create a reusable `base.html`.
- How to build the initial Blog layout.

---

# 1. What is a Django Template?

A Django Template is an HTML file that contains normal HTML along with Django Template Language (DTL).

It allows us to create dynamic webpages instead of writing every value directly inside Python code.

For example:

```html
<h1>{{ post.title }}</h1>
```

Here:

```text
{{ post.title }}
```

is a Django Template variable.

Django replaces it with the actual value provided by the View.

---

# 2. Why Do We Need Templates?

Earlier, we could return HTML directly from a View:

```python
return HttpResponse("<h1>Blog Home!</h1>")
```

This works, but it becomes difficult to manage large HTML pages.

For example, a complete website would contain:

- Navbar
- Header
- Footer
- Sidebar
- Blog Posts
- Forms
- CSS
- JavaScript

Putting all of this inside Python code would make the code difficult to read and maintain.

Instead, Django separates:

```text
Python Logic
      +
HTML Presentation
```

The Python code stays inside the View, while HTML is stored inside Templates.

---

# 3. `render()` Function

Django provides the `render()` shortcut for rendering templates.

Example:

```python
from django.shortcuts import render

def home(request):
    return render(request, 'blog/home.html')
```

The basic structure is:

```python
render(request, template_name)
```

When we need to send data:

```python
return render(request, 'blog/home.html', context)
```

---

# 4. Context

A Context is data that is passed from a View to a Template.

Example:

```python
context = {
    'posts': posts
}
```

Then:

```python
return render(request, 'blog/home.html', context)
```

The Template can now access:

```django
{{ posts }}
```

or loop through it:

```django
{% for post in posts %}
    ...
{% endfor %}
```

---

# 5. Blog Posts Data

At this stage, the blog posts are temporarily stored in Python.

Example:

```python
posts = [
    {
        'author': 'Corey Schafer',
        'title': 'Blog Post 1',
        'content': 'First post content',
        'date_posted': 'August 27, 2018'
    },
    {
        'author': 'Jane Doe',
        'title': 'Blog Post 2',
        'content': 'Second post content',
        'date_posted': 'August 28, 2018'
    }
]
```

This is temporary data.

Later in the tutorial, the posts will be stored in a database using Django Models.

---

# 6. Passing Posts to the Template

The View creates a context dictionary:

```python
context = {
    'posts': posts
}
```

Then sends it to the Template:

```python
return render(request, 'blog/home.html', context)
```

The complete flow is:

```text
posts list
    │
    ▼
context dictionary
    │
    ▼
render()
    │
    ▼
home.html
```

---

# 7. Template Variables

Django uses:

```django
{{ variable }}
```

to display values.

For example:

```django
{{ post.title }}
```

displays the title.

Similarly:

```django
{{ post.author }}
```

displays the author.

```django
{{ post.date_posted }}
```

displays the date.

```django
{{ post.content }}
```

displays the content.

---

# 8. Template For Loop

The blog contains multiple posts.

Instead of manually writing HTML for every post, Django's Template Language can loop through them.

Example:

```django
{% for post in posts %}
    <h1>{{ post.title }}</h1>
    <p>{{ post.author }} on {{ post.date_posted }}</p>
    <p>{{ post.content }}</p>
{% endfor %}
```

The loop means:

```text
For every post inside posts:

    Display title
    Display author
    Display date
    Display content
```

---

# 9. Django Template Tags

Django Template Language uses different syntax for different purposes.

## Variables

```django
{{ variable }}
```

Used to display data.

Example:

```django
{{ post.title }}
```

---

## Template Tags

```django
{% tag %}
```

Used for template logic.

Example:

```django
{% for post in posts %}
```

---

# 10. Template Inheritance

Template Inheritance is one of the most important concepts in this part.

Imagine that every page of the website needs:

- Same HTML structure
- Same Navbar
- Same Bootstrap CSS
- Same Sidebar
- Same CSS
- Same JavaScript

Without inheritance, we would have to copy all of this into every HTML file.

That creates duplicate code.

Template inheritance solves this problem.

---

# 11. `base.html`

We create a common parent template:

```text
base.html
```

It contains the common structure of the website.

For example:

```text
base.html
│
├── HTML structure
├── Bootstrap
├── CSS
├── Navbar
├── Main Container
├── Sidebar
└── Content Block
```

---

# 12. `{% block %}`

Inside `base.html`, we create a block:

```django
{% block content %}{% endblock content %}
```

This block is a placeholder.

It tells Django:

> Child templates can put their page-specific content here.

---

# 13. `{% extends %}`

A child template can inherit from `base.html`:

```django
{% extends "blog/base.html" %}
```

This means:

```text
home.html
    ↓
inherits
    ↓
base.html
```

The child template gets the common structure from the parent.

---

# 14. Child Template Example

`home.html`:

```django
{% extends "blog/base.html" %}

{% block content %}

    {% for post in posts %}
        <h1>{{ post.title }}</h1>
        <p>{{ post.author }} on {{ post.date_posted }}</p>
        <p>{{ post.content }}</p>
    {% endfor %}

{% endblock content %}
```

Notice that `home.html` does not contain:

```html
<html>
<head>
<body>
```

because those common parts already exist in `base.html`.

---

# 15. About Page

The same `base.html` can be reused for the About page.

Example:

```django
{% extends "blog/base.html" %}

{% block content %}

    <h1>About Page!</h1>

{% endblock content %}
```

Therefore:

```text
base.html
   │
   ├── home.html
   │
   └── about.html
```

Both pages share the same layout.

---

# 16. Template Inheritance Flow

```text
                 base.html
                     │
          ┌──────────┴──────────┐
          │                     │
          ▼                     ▼
      home.html             about.html
          │                     │
          ▼                     ▼
    Home Content           About Content
```

The final HTML is generated using the base template plus the child template's content.

---

# 17. Static Files

Static files are files that are served separately from dynamically generated page content.

Examples:

- CSS
- JavaScript
- Images

In this part, we use a CSS file:

```text
main.css
```

---

# 18. Static File Structure

The correct Django app structure is:

```text
blog/
│
├── static/
│   └── blog/
│       └── main.css
│
└── templates/
    └── blog/
        ├── base.html
        ├── home.html
        └── about.html
```

The extra `blog` directory inside `static` provides a namespace for the app's static files.

---

# 19. Why `static/blog/main.css`?

Suppose another Django app also has:

```text
main.css
```

For example:

```text
blog/static/blog/main.css
accounts/static/accounts/main.css
```

Django can distinguish them using the app namespace:

```text
blog/main.css
accounts/main.css
```

This reduces the possibility of static file name conflicts.

---

# 20. `{% load static %}`

Before using Django's static file tag, we load it:

```django
{% load static %}
```

This enables the `static` template tag.

---

# 21. Using `{% static %}`

The CSS file is linked using:

```html
<link rel="stylesheet" href="{% static 'blog/main.css' %}">
```

Django converts this into the appropriate static URL.

Conceptually:

```text
{% static 'blog/main.css' %}
            │
            ▼
       Static URL
            │
            ▼
       main.css
```

---

# 22. `main.css`

The custom CSS controls the appearance of the blog.

It contains styling for:

- Body
- Headings
- Navbar
- Content sections
- Article titles
- Article metadata
- Article images
- SVG icons

Example:

```css
body {
    background: #fafafa;
    color: #333333;
    margin-top: 5rem;
}
```

The `margin-top` is important because the navbar uses a fixed position.

---

# 23. Bootstrap

Bootstrap is used to create the responsive layout.

It provides pre-built CSS classes and components.

The project uses Bootstrap for:

- Navbar
- Grid
- Responsive layout
- Buttons
- Navigation
- Containers

---

# 24. Bootstrap Grid

The page is divided into two major sections:

```text
Main Content                  Sidebar
     8 columns                 4 columns
┌──────────────────────┬────────────────┐
│                      │                │
│    Blog Posts        │    Sidebar     │
│                      │                │
└──────────────────────┴────────────────┘
```

This is implemented using Bootstrap grid classes.

Conceptually:

```html
<div class="container">
    <div class="row">

        <div class="col-md-8">
            <!-- Blog Posts -->
        </div>

        <div class="col-md-4">
            <!-- Sidebar -->
        </div>

    </div>
</div>
```

---

# 25. Navbar

The base template contains a common navigation bar.

It provides links such as:

```text
Django Blog
Home
About
Login
Register
```

Because the navbar is inside `base.html`, it automatically appears on every page that extends `base.html`.

---

# 26. Sidebar

The blog layout contains a sidebar with sections such as:

```text
Our Sidebar

Latest Posts
Announcements
Calendars
etc.
```

The sidebar is placed in the common layout so it can be reused across pages.

---

# 27. Complete Architecture

At this point the application works approximately like this:

```text
                 Browser
                    │
                    ▼
             Project urls.py
                    │
                    ▼
               blog/urls.py
                    │
                    ▼
                 views.py
                    │
                    │ context
                    ▼
               home.html
                    │
                    │ extends
                    ▼
                base.html
                    │
          ┌─────────┼─────────┐
          │         │         │
          ▼         ▼         ▼
       Navbar    Sidebar    Content
                              │
                              ▼
                           posts
                              │
                              ▼
                           Browser
```

---

# 28. Important Difference: Template vs Static File

These two should not be confused.

## Templates

Contain HTML that Django renders dynamically.

```text
blog/templates/blog/
```

Example:

```text
home.html
about.html
base.html
```

---

## Static Files

Contain assets such as CSS, JavaScript, and images.

```text
blog/static/blog/
```

Example:

```text
main.css
```

So:

```text
Templates → HTML structure/content
Static → CSS/JS/images
```

---

# 29. Important Difference: View vs Template

### View

Python code.

Responsible for:

- Receiving request
- Preparing data
- Calling business logic
- Rendering a response

Example:

```python
def home(request):
    context = {
        'posts': posts
    }

    return render(request, 'blog/home.html', context)
```

### Template

HTML presentation.

Responsible for:

- Displaying data
- Page structure
- Template logic

Example:

```django
{% for post in posts %}
    <h1>{{ post.title }}</h1>
{% endfor %}
```

---

# 30. Important Difference: Project URLs vs App URLs

Project URL configuration:

```text
django_project/urls.py
```

connects requests to applications.

Example:

```python
path('', include('blog.urls'))
```

App URL configuration:

```text
blog/urls.py
```

connects URLs to views.

Example:

```python
path('', views.home, name='blog-home')
```

Flow:

```text
Project URL
     ↓
App URL
     ↓
View
```

---

# 31. Debugging: Static CSS 404

During this part, the browser showed an error similar to:

```text
'blog\main.css' could not be found
```

The requested URL was:

```text
/static/blog/main.css
```

The problem was not the CSS itself.

The problem was the physical file structure.

Correct structure:

```text
blog/
└── static/
    └── blog/
        └── main.css
```

After creating this structure, Django was able to find the CSS.

---

# 32. Debugging: Testing the Static File

A useful debugging technique was to open the CSS URL directly:

```text
http://127.0.0.1:8000/static/blog/main.css
```

If the CSS content is displayed, Django can find the static file.

If a 404 occurs, check:

```text
1. File location
2. static directory structure
3. {% load static %}
4. STATIC_URL
5. django.contrib.staticfiles
6. App registration
```

---

# 33. Debugging: Template Path

A common mistake is writing:

```python
return render(
    request,
    'blog/templates/blog/home.html'
)
```

This is incorrect when `templates` is already an app template directory.

The correct form is:

```python
return render(
    request,
    'blog/home.html'
)
```

Django's template loader searches the configured template directories.

---

# 34. Debugging: Root URL

Initially, the project URL could be configured as:

```python
path('blog_dev/', include('blog.urls'))
```

Then the blog would be available at:

```text
/blog_dev/
```

If we want the root URL like the tutorial:

```python
path('', include('blog.urls'))
```

Then:

```text
/
```

maps to the blog app.

---

# 35. Common Mistakes

## Mistake 1

Wrong:

```python
render(request, 'blog/templates/blog/home.html')
```

Correct:

```python
render(request, 'blog/home.html')
```

---

## Mistake 2

Wrong static location:

```text
blog/main.css
```

Correct:

```text
blog/static/blog/main.css
```

---

## Mistake 3

Forgetting:

```django
{% load static %}
```

before using:

```django
{% static 'blog/main.css' %}
```

---

## Mistake 4

Wrong URL prefix:

```python
path('blog_dev/', include('blog.urls'))
```

when the desired URL is:

```text
/
```

Use:

```python
path('', include('blog.urls'))
```

---

# 36. Modern Django Compatibility

The core concepts in this part remain valid in modern Django:

```text
render()
Template Inheritance
{% extends %}
{% block %}
{% for %}
{{ variable }}
{% load static %}
{% static %}
Static files
Context dictionaries
```

The original tutorial is based on an older Django version, so some generated project configuration and frontend dependencies may look different in a modern Django project.

The important approach is:

```text
Corey Concept
     ↓
Understand the concept
     ↓
Check current Django syntax
     ↓
Use modern compatible code where required
```

---

# 37. Best Practices

- Use `base.html` for common page structure.
- Use template inheritance instead of duplicating HTML.
- Keep CSS in static files.
- Namespace static files using the app name.
- Keep application logic in Python.
- Keep presentation logic in templates.
- Pass data through context.
- Use meaningful URL names.
- Keep each Django app organized.
- Do not unnecessarily modify Django configuration.

---

# 38. Interview Questions

### Basic

1. What is a Django Template?
2. What is Django Template Language?
3. What is the purpose of `render()`?
4. What is a context dictionary?
5. What does `{{ }}` mean in Django templates?
6. What does `{% %}` mean?

### Template Inheritance

7. What is Template Inheritance?
8. What is the purpose of `{% extends %}`?
9. What is the purpose of `{% block %}`?
10. Why should we use a `base.html`?

### Static Files

11. What are static files?
12. Why do we use `{% load static %}`?
13. What does `{% static %}` do?
14. What is the recommended static file structure inside a Django app?
15. Why is the app name included inside the static directory?

### Django Architecture

16. What is the difference between a View and a Template?
17. What is the difference between Project URLs and App URLs?
18. Explain the Django request-response flow.
19. How does data move from a View to a Template?
20. Why should HTML not be written directly inside Python Views for large pages?

---

# 39. Practice Questions

### Practice 1

Create a new:

```text
contact.html
```

template.

Make it inherit:

```text
base.html
```

---

### Practice 2

Create a `contact()` View.

Return the contact template using:

```python
render()
```

---

### Practice 3

Create a URL:

```text
/contact/
```

---

### Practice 4

Pass a title through context:

```python
context = {
    'title': 'Contact'
}
```

Display it using:

```django
{{ title }}
```

---

### Practice 5

Add a third blog post to the `posts` list.

Display it automatically using the existing:

```django
{% for post in posts %}
```

loop.

---

# 40. Quick Revision

## Templates

```text
HTML + Django Template Language
```

## Variables

```django
{{ variable }}
```

## Template Tags

```django
{% tag %}
```

## Rendering

```python
render(request, 'template.html', context)
```

## Inheritance

```django
{% extends "blog/base.html" %}
```

## Block

```django
{% block content %}
{% endblock content %}
```

## Static

```django
{% load static %}
```

## CSS

```html
<link rel="stylesheet" href="{% static 'blog/main.css' %}">
```

---

# 41. Final Revision Diagram

```text
                    USER
                     │
                     ▼
                  Browser
                     │
                     ▼
              Project urls.py
                     │
                     ▼
                blog/urls.py
                     │
                     ▼
                  View
                     │
                     │
                  Context
                     │
                     ▼
                 Template
                     │
              ┌──────┴──────┐
              │             │
              ▼             ▼
          base.html      home.html
              │             │
              ├─────────────┘
              │
              ├── Navbar
              ├── Bootstrap
              ├── Sidebar
              └── CSS
                     │
                     ▼
                Final HTML
                     │
                     ▼
                  Browser
```

---

# 🎯 Final Takeaway

The most important concept from this part is:

```text
View
  ↓
Context
  ↓
Template
  ↓
Rendered HTML
```

and:

```text
base.html
    ↓
Template Inheritance
    ↓
home.html / about.html
```

Django Templates allow us to keep **Python logic separate from HTML presentation**, while Template Inheritance allows us to build reusable layouts without repeating the same HTML code.

---

# 🚀 Part 03 Completed

Topics completed:

- Django Templates
- `render()`
- Context
- Template Variables
- Template Loops
- Template Inheritance
- `{% extends %}`
- `{% block %}`
- Static Files
- `{% load static %}`
- `{% static %}`
- Bootstrap
- Base Template
- Child Templates
- Blog Layout
- Sidebar
- Static File Debugging
- Template Debugging
- Request → View → Template → Response Flow

**Part 03 complete. 🚀**