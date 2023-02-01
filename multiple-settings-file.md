
# django project in multiple setting file

project in multiple setting file 


## document (refer link)

- [@refer link](https://simpleisbetterthancomplex.com/tips/2017/07/03/django-tip-20-working-with-multiple-settings-modules.html)


## steps

- create a settings folder with __init__.py file
- move settings file& rename it to base.py
- create a new development.py file
- import this line
```bash
  from .base import *
```

- after this we have to change manage.py 

```bash
  #before
      os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_react.settings')
  # after
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_react.settings.base')
```
- we have to settings folder in base.py 

- after this wsgi.py in chnages

```bash
  #before
      os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_react.settings')
  # after
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_react.settings.base')
```

## How to run
how to multiple setting file run
```bash
python manage.py runserver --settings=mysite.settings.development
```
