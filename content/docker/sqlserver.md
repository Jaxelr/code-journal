# Running sql server on docker

Make sure docker desktop is running, from the cmd line run:

`docker run --name sql_2019 -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=1Secure*Password1" -e "MSSQL_PID=Enterprise" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest`

The definition usage with docker compose is:

```yml
version: '3'
services:

  sqlserver:
    # For more details on configuring the Sql Server Docker image, see:
    #   https://hub.docker.com/_/microsoft-mssql-server
    image: mcr.microsoft.com/mssql/server:2019-latest

    # Expose the default Mysql port on localhost
    ports:
    - "1433:1433"
    container_name: sql_2019

    environment:
    - ACCEPT_EULA=Y
    - SA_PASSWORD=1Secure*Password1
    - MSSQL_PID=Enterprise
```

To connect to sql instance from command line:

`docker exec -it sql_2019 /opt/mssql-tools/bin/sqlcmd -S localhost -U sa`

To check if the container is accepting connections you can check the logs:

`docker logs sql_2019 | tail -n 10`