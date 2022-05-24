
# heroku in deploy python project


 - [refer link](https://dev.to/undefinedzack/how-to-deploy-a-django-app-to-heroku-3k6i)

## Steps

1) First ubantu in system in

```bash
curl https://cli-assets.heroku.com/install.sh | sh
```

2) Check version
```bash
heroku --version
```

3) After project in root dir in run command

```bash
heroku login
```

4) Creating a Heroku app

```bash
heroku create

```

It'll create a Heroku app with any random name. In my case it's "salty-peak-80429".

after this 
```bash
heroku git:remote -a salty-peak-80429
```
5) Setting up App server
```bash
pip install gunicorn
```
Let's test our app server. Locate the wsgi.py file in your main app directory, in my case my main directory is 'tutorial'

```bash
gunicorn tutorial.wsgi
```
6) Create 2 more files
In order to tell Heroku these thing's we'll have to create 2 more files :

a) Procfile 

b) requirements.txt

In the main directory which contains 'manage.py', we create Procfile

```bash
touch Procfile
```
Now we'll have to write commands which heroku should execute on app startup, this includes starting up app server.

```bash
web: gunicorn tutorial.wsgi
```

Creating Requirements.txt

```bash
pip freeze > requirements.txt

```

git add . and
git commit -m "added gunicorn (app server) with requirements.txt and Procfile"

Let's push it

```bash
git push heroku master
```

# if any error accour
* This file generate

```
runtime.txt 
```
==> file in code
python-3.8.10 
specific python version install
