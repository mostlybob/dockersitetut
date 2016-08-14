# Build your own images

This should track with https://docs.docker.com/engine/tutorials/dockerimages/

Starting work at https://docs.docker.com/engine/tutorials/dockerimages/#updating-and-committing-an-image
(much of the stuff til now 

I think the doc might be a bit outdated. I'm running into trouble installing the json gem, since it requires > ruby 2.0, but the version of ruby installed is 1.9.3. Things go downhill after that in the tutorial, but I get the gist of what they're saying. I'll try deleting the container and starting over.

## Detour

For the record, since removing an image was not as straightforward as I was expecting, here's what I ended up having to do:

```
$ docker ps
```

showed no containers running

```
$ docker images
```

listed them, showing `training/sinatra` as expected. Note the image id.

```
$ docker ps -a
```

shows similar info, if more verbose.

```
$ docker rmi training/sinatra
```

removes the image, but I was getting the error:

```
Error response from daemon: conflict: unable to remove repository reference "training/sinatra" (must force) - container 1693aff08ca7 is using its referenced image 49d952a36c58
```
so running:

```
$ docker rm 1693aff08ca7
```
fixed that. Now running

```
$ docker rmi training/sinatra
```

deleted the image.

## Carrying on

I'm going to try the defaults instead of specifying the version of ruby, see if that helps.

```
$ docker pull training/sinatra
```

did the pull, as expected.

```
$ docker images 
```

shows the image was created 2 y ago (today is 2016-08-14), so we'll see how this goes.

## Back to the tutorial

It looks like building off the `training/sinatra` image coming off the hub won't work. It's built off trusty, which is ruby 1.9 (after apt-get update/upgrade):

```
root@f78b24bb7d44:/# ruby --version
ruby 1.9.3p484 (2013-11-22 revision 43786) [x86_64-linux]
root@f78b24bb7d44:/# 
```

Running the command `apt-get install -y ruby2.0-dev` doesn't appear do do anything:

```
root@f78b24bb7d44:/# ruby --version
ruby 1.9.3p484 (2013-11-22 revision 43786) [x86_64-linux]
root@f78b24bb7d44:/# ruby2.0 --version
bash: ruby2.0: command not found
root@f78b24bb7d44:/# ruby2            
bash: ruby2: command not found
root@f78b24bb7d44:/# gem2
bash: gem2: command not found
root@f78b24bb7d44:/# gem2.0
bash: gem2.0: command not found
```

so I'm skipping working with the prepackaged container and moving to building an image from a Dockerfile.





-------


