
# Docker In Debugger

How to Docker in Debugger set 


## 🔗  Reference Site

 - [Docker In Debugger Reference](https://hackernoon.com/debugging-using-pdb-in-dockerized-environment-i21n2863)
 


## Steps
`docker-compose.yml` (or your docker-compose configuration) File in add some code

```bash
version: '3'

services:
   web:
    build: .
    volumes:
      - .:/app
    stdin_open: true   # Add this line into your service
    tty: true   # Add this line into your service
```

After those lines are added, start your Docker container as usual. In my case, I run:

```bash
docker-compose up -d
```
Once your Docker container is running, attach your terminal standard streams to your running container:

```bash
docker attach <your_container_id>
```

To find `<your_container_id>` in system:

```bash
docker ps
```

After all this write `debugger` in your script:

```bash
 def create(self, validated_data):
        import pdb; pdb.set_trace()
        is_test = validated_data.pop('is_test')
        countries = validated_data.pop('countries')
        bvis_user = validated_data.pop('bvis_user')
```
