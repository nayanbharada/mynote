
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
## How to run
how to multiple setting file run
```bash
python manage.py runserver --settings=mysite.settings.development
```
