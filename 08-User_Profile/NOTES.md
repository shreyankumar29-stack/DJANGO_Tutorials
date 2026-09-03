# Notes -- Video 8: User Profile & Picture

## 1. User Profile

Django's built-in `User` model can be extended using a separate
`Profile` model.

``` python
class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    image = models.ImageField(default='default.jpg', upload_to='profile_pics')
```

-   `OneToOneField` creates a one-to-one relationship between User and
    Profile.
-   Each user can have one profile.
-   The profile stores additional user information such as a profile
    picture.

## 2. Profile Picture

`ImageField` is used to store profile pictures.

``` python
image = models.ImageField(
    default='default.jpg',
    upload_to='profile_pics'
)
```

Uploaded images are stored in:

``` text
media/profile_pics/
```

A default image is used when a user has not uploaded a custom picture.

## 3. Pillow

Pillow is required for Django `ImageField`.

``` powershell
python -m pip install Pillow
```

## 4. Media Configuration

In `settings.py`:

``` python
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
MEDIA_URL = '/media/'
```

During development, media files are served through the project's URL
configuration.

## 5. Profile Template

The profile picture is displayed using:

``` html
<img class="rounded-circle account-img" src="{{ user.profile.image.url }}">
```

User information is displayed using:

``` html
<h2 class="account-heading">{{ user.username }}</h2>
<p class="text-secondary">{{ user.email }}</p>
```

## 6. Django Signals

Signals allow Django to automatically perform an action when a User is
created or saved.

The profile system uses signals to automatically create a Profile for a
newly created User.

``` text
User Created
     ↓
post_save Signal
     ↓
Profile Created
     ↓
Default Image Assigned
```

## 7. Default Profile Image

The default image is stored in:

``` text
media/profile_pics/default.jpg
```

The working database value was verified with:

``` python
Profile.objects.get(user__username='NewUser').image.name
```

Output:

``` text
'profile_pics/default.jpg'
```

## 8. Important Debugging Point

If a user exists but:

``` python
Profile.objects.get(user__username='NewUser')
```

raises:

``` text
Profile.DoesNotExist
```

then the User exists but its Profile has not been created.

If Signals are configured correctly, newly created users should
automatically receive a Profile.

## 9. Key Concepts Learned

-   One-to-One relationships
-   Django `ImageField`
-   Pillow
-   Media files
-   `MEDIA_ROOT`
-   `MEDIA_URL`
-   Django Signals
-   `post_save`
-   Automatic Profile creation
-   Default profile images
-   Django Shell debugging
