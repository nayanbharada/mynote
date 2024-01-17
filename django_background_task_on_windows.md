
# Django background schduler for windows

on windows we have similar to celery Django background schduler.

## Acknowledgements

 - [Reference link](https://pypi.org/project/django4-background-tasks/)
 - [Ref Demo link](https://medium.com/@robinttt333running-background-tasks-in-django-f4c1d3f6f06e)


```
  pip install django4-background-tasks
```

- This lib is used for new django versions and windows os in schedule background task


## Steps

- First we need to add pip lib for that
```
  pip install django4-background-tasks
```

- After that you need to change some code in settings.py

```
  INSTALLED_APPS = [
  .....,
  'background_task',
  .......
  ]
```

```
pip install migrate
```
- After this command execute 2 tables is create on django admin


- After that you need to create cron.py file for background job

- here example of cron per day which time you want to execute that cron
```
from background_task import background
from background_task.models import Task
from datetime import datetime

# @background(schedule=today_midnight,remove_existing_tasks=True)
@background(schedule=abs(datetime.now() - datetime.now().replace(minute=11, second=0, hour=11)),remove_existing_tasks=True)
def send_email():
    print("task call")
    
    print("task end")
    return None

send_email()

```
- here send_email() is background function call

- after this you need to change on app.py file as well

```
from django.apps import AppConfig


class VoteUpConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'vote_up'

    def ready(self):
        from . import cron
```

- app.py in ready method in file call so server reload time automatically background schedule


- if you want execute from views.py

```
from background_task import background
from django.contrib.auth.models import User

@background(schedule=60)
def notify_user(user_id):
    # lookup user by id and send them a message
    user = User.objects.get(pk=user_id)
    user.email_user('Here is a notification', 'You have been notified')


notify_user(user.id)
```
- notify_user(user.id) is call from views.py so  notify_useris called from background after 60 seconds
