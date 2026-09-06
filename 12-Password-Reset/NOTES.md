# Django Tutorial -- Video 12 Notes

## 1. Password Reset

Django provides built-in authentication functionality for password
reset.

``` text
Password Reset Request
        ↓
Enter Email
        ↓
Password Reset Email
        ↓
Open Reset Link
        ↓
Set New Password
        ↓
Password Reset Complete
```

## 2. Built-in Password Reset Views

Common Django views: - `PasswordResetView` - `PasswordResetDoneView` -
`PasswordResetConfirmView` - `PasswordResetCompleteView`

## 3. Typical URL Patterns

``` python
path(
    'password-reset/',
    PasswordResetView.as_view(
        template_name='users/password_reset.html'
    ),
    name='password_reset'
)

path(
    'password-reset/done/',
    PasswordResetDoneView.as_view(
        template_name='users/password_reset_done.html'
    ),
    name='password_reset_done'
)

path(
    'password-reset-confirm/<uidb64>/<token>/',
    PasswordResetConfirmView.as_view(
        template_name='users/password_reset_confirm.html'
    ),
    name='password_reset_confirm'
)

path(
    'password-reset-complete/',
    PasswordResetCompleteView.as_view(
        template_name='users/password_reset_complete.html'
    ),
    name='password_reset_complete'
)
```

## 4. SMTP Backend

For actual email delivery:

``` python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_PORT = 587
EMAIL_USE_TLS = True
```

## 5. Environment Variables

In `settings.py`:

``` python
EMAIL_HOST_USER = os.environ.get('EMAIL_USER')
EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_PASS')
```

In the root `.env`:

``` env
EMAIL_USER=yourgmail@gmail.com
EMAIL_PASS=your_app_password
```

## 6. Loading `.env`

Install:

``` powershell
python -m pip install python-dotenv
```

Then:

``` python
from dotenv import load_dotenv

load_dotenv(
    os.path.join(
        BASE_DIR,
        '..',
        '..',
        '.env'
    )
)
```

## 7. Console vs SMTP

Console backend prints the email in the terminal:

``` python
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
```

SMTP backend sends through the configured SMTP server:

``` python
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
```

## 8. Gmail App Password

Use a Google App Password for Gmail SMTP authentication. Treat it as a
secret.

## 9. Common Problems

If email does not arrive, check: - The Django user has the correct
registered email. - SMTP backend is configured. - App Password is
correct. - `.env` is loaded. - Spam/Promotions folders. - Terminal for
SMTP errors.

Test configuration:

``` powershell
python manage.py shell
```

``` python
from django.conf import settings
print(settings.EMAIL_HOST_USER)
print(bool(settings.EMAIL_HOST_PASSWORD))
```

Expected:

``` text
yourgmail@gmail.com
True
```

## 10. Key Takeaways

-   Django provides built-in password-reset views.
-   SMTP is used for real email delivery.
-   Gmail SMTP uses port 587 with TLS.
-   Keep secrets outside source code.
-   `.env` should be ignored by Git.
-   The Django account must have a registered email.
