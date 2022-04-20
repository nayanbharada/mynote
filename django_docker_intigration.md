
# Django Project Docker

django project in docker intigration


## Documentation (reference link)

[Documentation](https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/)


## create a virtualenv & project

To deploy this project run

```bash
virtualenv venv --python=python3.6
source venv/bin/activate
pip install django
django-admin.py startproject hello_django
cd hello_django/
python manage.py migrate
python manage.py runserver
pip freeze > requirements. txt

```

## for ubantu(20.4) in first install

```bash
sudo snap install docker
sudo apt  install docker-compose
```
## create a Dockerfile
- set working directory proper
```bash
# pull official base image
FROM python:3.6-alpine

# set work directory
WORKDIR /usr/src/

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# copy project
COPY . .

```

## create docker-compose.yml file
```bash
version: '3.2'

services:
  web:
    build: ./
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - ./app/:/usr/src/app/
    ports:
      - 8000:8000
    env_file:
      - ./.env

```

## for .env file

```bash
nano .env
```
- add this value in .env file
```bash
DEBUG=1
SECRET_KEY=foo
DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1]
```

## for django settings file

```bash
SECRET_KEY = os.environ.get("SECRET_KEY")

DEBUG = int(os.environ.get("DEBUG", default=0))

# 'DJANGO_ALLOWED_HOSTS' should be a single string of hosts with a space between each.
# For example: 'DJANGO_ALLOWED_HOSTS=localhost 127.0.0.1 [::1]'
ALLOWED_HOSTS = os.environ.get("DJANGO_ALLOWED_HOSTS").split(" ")
```

## for docker run 
- manage.py file path through run

```bash
docker-compose build
docker-compose up
```
