# Django Tutorial -- Video 12: Email and Password Reset

## Overview

This part continues the Django Blog project from Video 11 and adds
password-reset functionality using Django's built-in authentication
views and email system.

## What We Learned

-   Password reset requests and the complete reset flow
-   Django built-in password reset views
-   Password reset email configuration
-   Gmail SMTP configuration
-   Using a `.env` file for email credentials
-   Loading environment variables with `python-dotenv`
-   Password reset templates and URLs

## Project Structure

``` text
DJANGO_Tutorials/
├── .env
├── .gitignore
└── 12-Password-Reset/
    └── django_project/
        ├── manage.py
        ├── db.sqlite3
        ├── blog/
        ├── users/
        └── django_project/
            └── settings.py
```

## Email Configuration

``` python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
EMAIL_HOST_USER = os.environ.get('EMAIL_USER')
EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_PASS')
```

Root `.env`:

``` env
EMAIL_USER=yourgmail@gmail.com
EMAIL_PASS=your_16_character_app_password
```

The `.env` file must not be committed to Git.

## Password Reset Flow

1.  User opens the password-reset page.
2.  User enters the registered email address.
3.  Django generates a password-reset link.
4.  Django sends the email through Gmail SMTP.
5.  User opens the link.
6.  User sets a new password.
7.  Django confirms the password change.

## Testing

``` powershell
python manage.py check
python manage.py runserver
```

Open:

``` text
http://127.0.0.1:8000/password-reset/
```

Use an email address registered with the Django user account.

## Security

-   Never commit `.env`.
-   Never share the Gmail App Password.
-   Use a Google App Password instead of the normal Gmail password.

## Status

**Completed -- Video 12**
