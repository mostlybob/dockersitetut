# Manage data in containers

https://docs.docker.com/engine/tutorials/dockervolumes/

## Observations
I spent a lot of time poking around trying to understand the relationship between the host and the running container(s) with regard to volumes. There's a host folder at `/var/lib/docker/volumes/` which holds the files that serve as volumes. There's a binary metadata.db file which presumably is used by the docker daemon to manage the files as volumes. 

I'm still getting my head around some of the command line switches, but `docker <command> --help` is usually just a few keystrokes away. :-)

I still haven't quite found a way to list and manage the containers from a command prompt. I'm sure it's there; I just haven't found it.
