
# .bat file creation 

for virtual env activate and python manage.py runserver

## File code


```bash
@echo off
cmd /k "cd /d D:\projects\virtual_envs\FOREX_VENV\Scripts & activate & cd /d    D:\projects\FOREX_TRACKER\Project\Forex_Tracker & python manage.py runserver" 

```


- here D:\projects\virtual_envs\FOREX_VENV\Scripts is the virtual env location and activate the virtual env

- D:\projects\FOREX_TRACKER\Project\Forex_Tracker project location 

- python manage.py runserver is command for runserver


