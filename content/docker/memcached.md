# Running memcached on docker

Make sure docker desktop is running.

From the cmd line run:

`docker run --name memecached -p 11211:11211 -d memcached memcached -m 64`

For more information check [docker hub](https://hub.docker.com/_/memcached)
