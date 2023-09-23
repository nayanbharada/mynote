# Django Web Production For Static Files & Error Pages 

Django website production on live time static file changes and dynamic error pages ex. 404, 500 

## Pre Requirements
```bash
  pip install whitenoise
```
## steps
- First Settings.py in set Debug=False set
- After this you need to set STATIC_ROOT 
- you need to add whitenoise in middleware
- and last step you need to run command python manage.py collectstatic


## Settings.py in changes
- Settings.py file in set for production

```bash
  DEBUG = False
```

- second steps you need to add STATIC_ROOT

```bash
STATICFILES_DIRS = (
    Path.joinpath(BASE_DIR, "static"),
)
STATIC_URL = '/static/'
STATIC_ROOT = Path.joinpath(BASE_DIR, 'staticfiles')
```

- we need to install whitenoises
- after installation we need to add in middleware
- This should be added just below the 'django.middleware.security.SecurityMiddleware' and above all the remaining middleware. So that your middleware list will look like this:-

```bash
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware', #after this line
    'whitenoise.middleware.WhiteNoiseMiddleware', #add it exactlyhere
    'django.contrib.sessions.middleware.SessionMiddleware', #before this
    '...'
]
```


## Urls.py in changes
- We are add STATIC_ROOT so we need to add root url(project urls.py) file in add this lines

```bash
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

## Final run

```bash
python manage.py collectstatic
```

## Last step
- last step execute the server again and hard refresh the browsers
```bash
python manage.py runserver
```
