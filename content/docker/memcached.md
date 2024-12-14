# Running memcached on docker

Make sure docker desktop is running.

From the cmd line run:

`docker run --name memecached -p 11211:11211 -d memcached memcached -m 64`


Optionally using a yml configuration file:

```yml
services:

  memcached:
    # For more details on configuring the Memcahed Docker image, see:
    #   https://hub.docker.com/_/memcached
    image: memcached

    # Expose the default Memcached port on localhost
    ports:
      - '11211:11211'
    container_name: memecached
```

For more information check [docker hub](https://hub.docker.com/_/memcached)
