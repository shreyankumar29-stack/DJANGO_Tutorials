# Video 8 -- User Profile & Picture

## Overview

This part continues the Django Blog project by implementing a complete
User Profile system with profile pictures.

The project extends Django's built-in `User` model using a separate
`Profile` model connected through a One-to-One relationship.

Django Signals are also used to automatically create a profile whenever
a new user is created.

## Objectives

-   Create a user profile system
-   Extend Django's built-in User model
-   Create a One-to-One relationship between User and Profile
-   Add profile picture functionality
-   Configure media files
-   Display profile information
-   Use Django Signals
-   Automatically create profiles for new users
-   Provide a default profile picture

## Technologies Used

-   Python
-   Django
-   SQLite
-   HTML
-   CSS
-   Bootstrap
-   Pillow
-   Django Crispy Forms

## Concepts Covered

### Profile Model

``` python
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    image = models.ImageField(
        default='default.jpg',
        upload_to='profile_pics'
    )

    def __str__(self):
        return f'{self.user.username} Profile'
```

The `OneToOneField` ensures that each user has one corresponding
profile.

### Profile Pictures

``` python
image = models.ImageField(
    default='default.jpg',
    upload_to='profile_pics'
)
```

Uploaded profile pictures are stored inside `media/profile_pics/`.

A default profile image is used for users who have not uploaded a custom
picture.

### Media Configuration

``` python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

Media URLs are configured in the project's URL configuration during
development.

### Django Signals

Django Signals automatically create a Profile when a User is created.

``` text
User Created
     ↓
Signal Triggered
     ↓
Profile Created
     ↓
Default Profile Picture Assigned
```

### Profile Page

The profile page displays the profile picture, username, and email
address.

``` html
<img class="rounded-circle account-img"
     src="{{ user.profile.image.url }}">

<h2 class="account-heading">
    {{ user.username }}
</h2>

<p class="text-secondary">
    {{ user.email }}
</p>
```

## Project Structure

``` text
08-User_Profile/
└── django_project/
    ├── blog/
    ├── users/
    │   ├── migrations/
    │   ├── templates/
    │   │   └── users/
    │   │       └── profile.html
    │   ├── admin.py
    │   ├── apps.py
    │   ├── forms.py
    │   ├── models.py
    │   ├── signals.py
    │   └── views.py
    ├── django_project/
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    ├── media/
    │   └── profile_pics/
    │       └── default.jpg
    ├── db.sqlite3
    ├── manage.py
    ├── COMMANDS.md
    ├── NOTES.md
    └── README.md
```

## Application Flow

``` text
User Registration
       ↓
Django User Created
       ↓
post_save Signal
       ↓
Profile Automatically Created
       ↓
Default Profile Image Assigned
       ↓
Profile Page
       ↓
Username + Email + Profile Picture
```

## Testing

The implementation was tested by creating a new user and checking
whether a Profile was automatically generated.

Using Django Shell:

``` python
from users.models import Profile

Profile.objects.get(
    user__username='NewUser'
).image.name
```

Expected result:

``` text
profile_pics/default.jpg
```

This confirms that the User exists, the Profile exists, Signals are
working, and the default profile image is assigned correctly.

## Compatibility Notes

This project follows Corey Schafer's Django Blog tutorial, which was
originally created for an older Django version.

The current environment uses a newer Django version, so some behavior
can differ from the original tutorial. The implementation has been
adjusted where necessary while keeping the tutorial's original concepts
and structure.

## Key Learnings

-   Extending Django's User model
-   Using `OneToOneField`
-   Working with `ImageField`
-   Handling Django media files
-   Configuring `MEDIA_ROOT` and `MEDIA_URL`
-   Understanding Django Signals
-   Using `post_save` to automate related model creation
-   Using Django Shell for debugging
-   Using default images with `ImageField`

## Future Improvements

-   Allow users to update their profile
-   Allow users to upload custom profile pictures
-   Add image validation
-   Add image size restrictions
-   Add profile editing functionality
-   Improve profile page UI
-   Add additional profile information

## Status

**Video 8 -- User Profile & Picture: Completed**

Implemented features:

-   User Profile
-   Profile Picture
-   Default Profile Picture
-   Media Configuration
-   One-to-One User/Profile Relationship
-   Django Signals
-   Automatic Profile Creation
-   Profile Display

## Reference

This part is based on the Django Blog tutorial by Corey Schafer and is
maintained as a learning/reference project.

## Author

**Shreyansh**

Django Learning Project\
Part of the Django Tutorial Series
