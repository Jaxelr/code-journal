# Running sql server on docker

Make sure docker desktop is running, from the cmd line run:

`docker run --name sqlserver -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=1Secure*Password1" -e "MSSQL_PID=Enterprise" -p 1433:1433 -d mcr.microsoft.com/mssql/server:2019-latest`

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
    container_name: sqlserver

    environment:
      ACCEPT_EULA: 'Y'
      SA_PASSWORD: '1Secure*Password1'
      MSSQL_PID: 'Enterprise'
```

To connect to sql instance from command line:

`docker exec -it sql_2019 /opt/mssql-tools/bin/sqlcmd -S localhost -U sa`

To check if the container is accepting connections you can check the logs:

`docker logs sql_2019 | tail -n 10`


## Known issues

While working with the Appveyor CI i ran into the following error:

`sqlservr: This program requires a machine with at least 2000 megabytes of memory.`

This is a known issue on the [mssql-docker repo](https://github.com/Microsoft/mssql-docker/issues/293)

As a workaround, i tested the image using the following [repository](https://github.com/justin2004/mssql_server_tiny) and it works as intended.

As another workaround, use the github ci, since it does not have the same limitation.
