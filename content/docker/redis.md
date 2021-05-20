# Running Redis on docker

Make sure docker desktop is running.

From the cmd line run:

`docker run -p 6379:6379 redis --name redisito`

Optionally using a yml configuration file:

```yml
version: '3'
services:

  redis:
    # For more details on configuring the Redis Docker image, see:
    #   https://hub.docker.com/_/redis
    image: redis

    # Expose the default Mysql port on localhost
    ports:
    - "6379:6379"
    container_name: redisito
```

For more information check [docker hub](https://hub.docker.com/_/redis/)
