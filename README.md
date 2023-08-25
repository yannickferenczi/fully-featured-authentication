# Fully Featured Authentication system

- Install django

    `pip install django`

- Install django-allauth

    `pip install django-allauth`


- Create a django project

    `django-admin startproject authentication .`

- Add the following to settings.py

    ```Python
    AUTHENTICATION_BACKENDS = [
    # Needed to login by username in Django admin, regardless of `allauth`
    'django.contrib.auth.backends.ModelBackend',

    # `allauth` specific authentication methods, such as login by email
    'allauth.account.auth_backends.AuthenticationBackend',

    ]
    ```

    ```Python
    INSTALLED_APPS = [
    ...
    # The following apps are required:
    'django.contrib.auth',
    'django.contrib.messages',

    'allauth',
    'allauth.account',
    'allauth.socialaccount',
    # ...and include the providers you want to enable:
    ```

- Add the path to urls.py

    ```Python
    from django.urls import path, include

    urlpatterns = [
    path('accounts/', include('allauth.urls')),
    ]
    ```

- Create the database tables

    `python3 manage.py migrate --plan`
    
    - then if everything ok:
    
    `python3 manage.py migrate`

- Create a superuser

    `python3 manage.py createsuperuser`

- Run the project

    `python3 manage.py runserver`

    - it might show an error *_DisallowedHost at /_*, then add the following

    `ALLOWED_HOSTS = ['8000-yannickferenczi-fully-fe-iapagkgdhs.us2.codeanyapp.com']`

    - if you get an error Forbidden, csrf verification failed, add the following

    `CSRF_TRUSTED_ORIGINS = ['https://8000-yannickferenczi-fully-fe-iapagkgdhs.us2.codeanyapp.com']`

- To personalize the authentication, add some configuration to settings.py

    ```Python
    ACCOUNT_EMAIL_REQUIRED = True
    ACCOUNT_AUTHENTICATION_METHOD = 'email'
    ACCOUNT_CHANGE_EMAIL = True
    ACCOUNT_CONFIRM_EMAIL_ON_GET = True
    ACCOUNT_EMAIL_VERIFICATION = 'mandatory'
    ACCOUNT_EMAIL_SUBJECT_PREFIX = 'Subject-Prefixe'

    ACCOUNT_DEFAULT_HTTP_PROTOCOL = 'https'  # See more details

    ACCOUNT_LOGIN_ON_EMAIL_CONFIRMATION = True
    ACCOUNT_LOGOUT_ON_PASSWORD_CHANGE = True
    ACCOUNT_USERNAME_REQUIRED = False
    ```
