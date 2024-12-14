# Running postgres on docker

Make sure docker desktop is running.

From the cmd line run:

`docker run --name=postgres -p 5432:5432 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=postgres -d postgres:12.4-alpine`

_Optionally_ you can use a yml configuration file:

```yml
services:

  postgres:
    # For more details on configuring the Postgres Docker image, see:
    #   https://hub.docker.com/_/postgres/
    image: postgres:13-alpine

    # Expose the default Postgres port on localhost
    ports:
      - '5432:5432'
    network_mode: bridge
    container_name: postgres

    environment:
      POSTGRES_USER: 'postgres'
      POSTGRES_PASSWORD: 'Password12'
      POSTGRES_DB: 'postgres'

    # Optional: Copy files from initdb path into the image so that they will be run on boot
    volumes:
      - ./initdb:/docker-entrypoint-initdb.d
```

You can check the following [github](https://github.com/Jaxelr/postgres-docker-tutorial) for more examples.

To find the ip being used you can run one of the following commands:

`docker inspect postgres | grep IPAddress`

or

`docker inspect -f "{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" postgres`

To check if the container is accepting connections you can check the logs:

`docker logs postgres | tail -n 2`

The config usage for the webconfig is:

```csharp
var connection = new NpgsqlConnection("Server=localhost;Port=5432;Database=postgres;Username=postgres;Password=postgres;");
```
