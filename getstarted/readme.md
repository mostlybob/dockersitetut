#Getting Started

After being sure it's installed. I'm on Korora, which is a Fedora derivative, and the docs for that are at https://docs.docker.com/engine/installation/linux/fedora/

## Getting it going

`sudo systemctl start docker`

I'm not sure how heavy the daemon is, but I suppose I could put it on the startup stuff. To do that, here's the deal:

`sudo systemctl enable docker`

## Creating the Group

Check for the existence of the group:

`getent group docker`

If it's not there, create it!

`sudo groupadd docker`

And add a user:

`sudo usermod -aG docker <your_username>`

Docs say relog, so do that, if you had to create the group/user.

There's stuff there about uninstalling, but let's assume I want to keep it for now.

## Running it

There are two steps, getting the image and running it:

`$ docker pull ubuntu`

This pulls the image, but doesn't run it.

`docker run -i -t ubuntu /bin/bash '

The result is a command prompt that is running the shell in the image.

From the docs:

The `-i` flag starts an interactive container. The `-t` flag creates a pseudo-TTY that attaches `stdin` and `stdout`.
The image is `ubuntu`. The command `/bin/bash` starts a shell you can log in.

To detach the `tty` without exiting the shell, use the escape sequence `Ctrl-p + Ctrl-q`. The container continues to exist in a stopped state once exited. To list all running containers, run `docker ps`. To view stopped and running containers, run `docker ps -a`.

(There's a lot of stuff here, probably more than I really need, but it's there.)

## Listing containers

```
$ docker ps # Lists only running containers
$ docker ps -a # Lists all containers
```

## Controlling containers

```
# Start a new container
$ JOB=$(docker run -d ubuntu /bin/sh -c "while true; do echo Hello world; sleep 1; done")

# Stop the container
$ docker stop $JOB

# Start the container
$ docker start $JOB

# Restart the container
$ docker restart $JOB

# SIGKILL a container
$ docker kill $JOB

# Remove a container
$ docker stop $JOB # Container must be stopped to remove it
$ docker rm $JOB
```

(There's stuff here about saving state. I think for what I'm looking at some of this can be handled with version control. )





-----------------
