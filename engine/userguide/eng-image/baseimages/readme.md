# Creating a base image

https://docs.docker.com/engine/userguide/eng-image/baseimages/

The first bit assumes I'm running Ubuntu or at least some Debian variant, since it wants `debootstrap` and I don't have that, obviously. I don't think I'd be doing much building using `tar` anyway. There are other scripts they link to which look interesting. Maybe something to keep in mind for later, but it looks more advanced than what I'm looking for right now.

The example building a simple image based off `scratc` is more my speed. Although the build doesn't seem to want to go:

```
$ docker build .
Sending build context to Docker daemon 16.38 kB
Step 1 : FROM scratch
 ---> 
Step 2 : ADD hello /
lstat hello: no such file or directory
```

Maybe look at the repo at https://github.com/docker-library/hello-world for some guidance.

-----
