# Video 9 -- Update User Profile

## Overview

This part continues the Django Blog project by adding functionality to
update user account and profile information. It builds on the User
Profile and Picture functionality from Video 8.

## Objectives

-   Update user account information
-   Update profile information
-   Work with multiple forms on one page
-   Handle profile picture uploads
-   Resize profile images
-   Use Pillow for image processing
-   Customize the model `save()` method

## Technologies Used

-   Python
-   Django
-   SQLite
-   HTML
-   Bootstrap
-   Pillow
-   Django Crispy Forms

## Concepts Covered

### User and Profile Forms

The profile page handles Django `User` information and custom `Profile`
information so users can update account details and their profile
picture.

### Image Processing

Pillow is used to open and resize uploaded images.

``` python
from PIL import Image

img = Image.open(self.image.path)

if img.height > 300 or img.width > 300:
    output_size = (300, 300)
    img.thumbnail(output_size)
    img.save(self.image.path)
```

### Custom Model Save Method

``` python
def save(self, *args, **kwargs):
    super().save(*args, **kwargs)

    img = Image.open(self.image.path)

    if img.height > 300 or img.width > 300:
        output_size = (300, 300)
        img.thumbnail(output_size)
        img.save(self.image.path)
```

## Important Compatibility Fix

The correct Pillow import is:

``` python
from PIL import Image
```

Do not use:

``` python
from PIL.Image import Image
```

The wrong import can cause:

``` text
AttributeError: type object 'Image' has no attribute 'open'
```

## Project Structure

``` text
09-Update-User-Profile/
└── django_project/
    ├── blog/
    ├── users/
    │   ├── migrations/
    │   ├── templates/
    │   ├── admin.py
    │   ├── apps.py
    │   ├── forms.py
    │   ├── models.py
    │   ├── signals.py
    │   └── views.py
    ├── django_project/
    │   ├── settings.py
    │   ├── urls.py
    │   └── ...
    ├── media/
    │   └── profile_pics/
    ├── db.sqlite3
    ├── manage.py
    ├── COMMANDS.md
    ├── NOTES.md
    └── README.md
```

## Testing

1.  Log in.
2.  Open `/profile/`.
3.  Update user information.
4.  Upload a profile picture.
5.  Submit the form.
6.  Confirm the updated information appears.
7.  Confirm the image is stored under `media/profile_pics/`.
8.  Test a large image to verify resizing.

## Key Learnings

-   Updating Django User data
-   Updating Profile data
-   Handling multiple forms
-   Uploading images
-   Using Pillow
-   Resizing images
-   Overriding model `save()`
-   Debugging image-related errors

## Status

**Video 9 -- Update User Profile: Completed**

Implemented: - User profile update - Profile update - Profile picture
upload - Image resizing - Pillow image processing - Form handling

## Reference

This part is based on the Django Blog tutorial by Corey Schafer and is
maintained as a learning/reference project.

## Author

**Shreyansh**

