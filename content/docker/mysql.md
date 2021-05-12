# Running mysql on docker

Make sure docker desktop is running.

From the cmd line run:

`docker run --name=mycutesql -p 3306:3306 -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -e MYSQL_DATABASE=test -e MYSQL_ROOT_HOST=% -d mysql`

_Optionally_ you can set a password, by default since this is local work i do not

The definition for usage with docker compose is:

```yml
version: '3'
services:

  mysql:
    # For more details on configuring the Mysql Docker image, see:
    #   https://hub.docker.com/_/mysql
    image: mysql/mysql-server:latest

    # Expose the default Mysql port on localhost
    ports:
    - "3306:3306"
    container_name: mycutesql

    environment:
    - MYSQL_ALLOW_EMPTY_PASSWORD=yes
    - MYSQL_ROOT_HOST=%
    - MYSQL_DATABASE=test
```

To find the ip being used you can run one of the following commands:

`docker inspect mycutesql | grep IPAddress`

or

`docker inspect -f "{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}" mycutesql`

To check if the container is accepting connections you can check the logs:

`docker logs mycutesql | tail -n 2`

The config should be something similar to:

```csharp
    var connection = new MySqlConnection("Server=127.0.0.1;Port=3306;Database=test;User Id=root;");
```
