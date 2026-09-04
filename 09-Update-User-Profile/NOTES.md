# Notes -- Video 9: Update User Profile

## 1. Purpose

Video 9 adds the ability to update user account and profile information
from the profile page.

## 2. Forms

Two types of information are handled:

-   Django `User` information
-   Custom `Profile` information

This allows the user to update account details and the profile picture.

## 3. Pillow

Pillow is used for image processing.

``` powershell
python -m pip install Pillow
```

Correct import:

``` python
from PIL import Image
```

## 4. Image Resizing

``` python
img = Image.open(self.image.path)

if img.height > 300 or img.width > 300:
    output_size = (300, 300)
    img.thumbnail(output_size)
    img.save(self.image.path)
```

## 5. Custom save()

``` python
def save(self, *args, **kwargs):
    super().save(*args, **kwargs)

    img = Image.open(self.image.path)

    if img.height > 300 or img.width > 300:
        output_size = (300, 300)
        img.thumbnail(output_size)
        img.save(self.image.path)
```

`super().save()` saves the model first, after which the saved image can
be opened and resized.

## 6. Important Error

If this appears:

``` text
AttributeError: type object 'Image' has no attribute 'open'
```

use:

``` python
from PIL import Image
```

and not:

``` python
from PIL.Image import Image
```

## 7. Media Location

Uploaded profile pictures are stored in:

``` text
media/profile_pics/
```

## 8. Testing Checklist

-   Login
-   Open `/profile/`
-   Update username/email
-   Select a profile image
-   Submit the form
-   Confirm updated information
-   Confirm image appears
-   Confirm uploaded image is inside `media/profile_pics/`
-   Test a large image to verify resizing

## 9. Key Concepts

-   Model forms
-   Multiple forms
-   File uploads
-   ImageField
-   Pillow
-   Image resizing
-   Model `save()`
-   Profile updates
