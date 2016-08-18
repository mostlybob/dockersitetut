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

Maybe look at the repo at https://github.com/docker-library/hello-world for some guidance. _That did it. There's a mismatch between what's in the docs and what's in the current version of the repo._

From the [repo](https://github.com/docker-library/hello-world/blob/master/hello-world/Dockerfile):

```
FROM scratch
COPY hello /
CMD ["/hello"]
```

Well, that didn't work either - same error. Hm. I'm sure I'm missing something pretty basic.

Getting there. The directive `COPY hello /` or `ADD hello /` relied on a binary blob named `hello` being present. I got that from the repo mentioned above and added that and the image built, but trying to run it gets an error:

```
docker: Error response from daemon: oci runtime error: exec: "/hello": permission denied.
```

so we're still seeing a permissions issue.


-----
