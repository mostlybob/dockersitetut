Having trouble getting the webapp example in the Docker docs to work, so I cloned the GH repo at https://github.com/docker-training/webapp

Running inside the repo:

```docker build -t webapp .```

After building run:

```docker run -d -P webapp python app.py```

- ```-d``` puts it in the background
- ```-P``` exposes the ports

Running ```docker ps``` shows, among other things, the exposed port, something like ```0.0.0.0:32769->5000/tcp``` 

Opening a browser to http://localhost:32769 shows the web app up and running

```docker run -d -p 80:5000  webapp python app.py```

will run the container with the exposed port available at port 80 locally

Other stuff from https://docs.docker.com/userguide/usingdocker/

```docker ps```
to get the names

```docker port <name> <exposed port>
- gets the local port for the container's exposed port(s)

```docker logs -f <name>```
- lists log entries on container

```docker top <name>```
- does a top on the container. Will require a ctrl-c to quit

```docker inspect <name>```
- returns JSON with configuration information on container

```docker inspect -f "{{.<section>.<subsection>}}" <name>```
- same as above for a particular section e.g. "{{.Config.Cmd}}"
- may return an array of settings e.g. {[python app.py]}

```docker rm <name>```
- removes a stopped container
- final and irreversible

Moving on to https://docs.docker.com/userguide/dockerimages/

```docker images```
- shows local cache of images

```docker pull <name>```
- pulls an image from the hub/repository

```docker search <search term>```
- search for an image

After running an image & making changes, commit 

```docker run -t -i training/sinatra /bin/bash```
- starts container - note the image label e.g. root@efd4985bdd64:/# has an image label of efd4985bdd64
- within container, make changes, install packages, etc
- exit

```docker commit -m "Added json gem" -a "Kate Smith" 0b2616b0e5a8 ouruser/sinatra:v2```
- an example commit, using -m for message, -a for committer, the label (see above) and a new user/image:tag

```docker images```
- to show

```docker run -t -i ouruser/sinatra:v2 /bin/bash```
- to run it

Docker images using ```Dockerfile```
- doc steps through creating a simple Dockerfile to create an Ubuntu image running Sinatra
- side references to 
  - https://docs.docker.com/reference/builder
  - https://docs.docker.com/articles/dockerfile_best-practices

```docker images```
- shows newly created image e.g. 

```
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
bob/sinatra         v2                  02c831b4cabc        4 minutes ago       318.6 MB
```

```docker run -t -i bob/sinatra:v2 /bin/bash```
- runs it





---
