# Docker Image for PostgreSQL and PgAdmim

You can create your own Docker image by using `Dockerfile` if there is no Docker image in [Docker Hub](https://hub.docker.com/) that suites your need.

## Dockerfile For PostgreSQL

The Dockerfile given creates the postgreSQL image by copying the License key and PostgreSQL respository for installing it. And it also creates a `User` with `Password` inside which creates an Empty Database which could help us in future steps.

For Building this Dockerfile in command Prompt use the below given command:

```
$ docker build -t (imageName) .
```
Example:
```
$ docker build -t img_postgresql .
```

Here, Option -t is used to name the image ascontentserverimage, image name should always be in lowercase alphabets and should not contain any spaces . This command could create a Docker image named `img_postgresql`.

You can check the image created using command 
    `$ docker images`

To Run this image:

```
$ docker run -it --name (containerName) (postgresQL_imageName)
```
Example:
```
$ docker run -it --name cont_postgresql img_postgresql
```

This will successfully create the PostgreSQL container named `cont_postgresql`. The Option '--name' is used to give the proper name to container which should not have any spaces between and the -Flag '-it' is used to  run container interactively and attached to your terminal.

Now, using the command `$ docker ps` you could see the container created/started in the name given (say cont_postgresql).

For Executing the Container:
```
$ docker exec -it (containerName) bash
```
Example:
```
$ docker exec -it cont_postgresql bash
```

This will create a new Bash session in the container cont_postgresql in terminal.

We can make use of this postgresql database in terminal itself. But for the user intraction we have to make use of postgresql-client. Here we are making use of popular client for PostgreSQL `pgAdmin`.

Now, you are inside the container and can execute the postgreSQL commands. The following basic postgresql command helps in authenticating and login to the postgres 

```
$ psql -h $PG_PORT_5432_TCP_ADDR -p $PG_PORT_5432_TCP_PORT -d docker -U docker --password
```

## Testing the Database Created

Once you have authenticated and will have a `docker =#` prompt and you can make use of the postgresql database. As mentioned above, to make sure that a empty database named `docker` is created you can see in the list of databases and can manipulate in it.

```
psql (9.3.1)
Type "help" for help.

$ \l
             List of Databases
|        Name      |         owner      |
|docker            |        docker      |
|postgres          |        postgres    |
|template0         |        postgres    |
|template1         |        postgres    |
```
Create a table in database `docker`:
```
$ docker=# CREATE TABLE cities (
docker(#     name            varchar(80),
docker(#     location        varchar(50)
docker(# );
CREATE TABLE
$ docker=# INSERT INTO cities VALUES ('Divya', 'India');
INSERT 0 1
$ docker=# select * from cities;
     name      | location
---------------+-----------
 Divya         | India
(1 row)
```

## PgAdmin
You can use the above created Docker Container in the terminal itself. In such case if we need a client interaction, we have to make use of any `Postgresql-client`. One such popular postgresql-client is `pgAdmin`. Creating a Container for pgAdmin and port-forwarding the PostgreSQL database to PgAdmin gives the User Interface for postgreSQL database.

Creating the pgAdmin image:
```
$ docker run --name (PgAdminName) -d -p (hostPort):(ContainerPort) fenglc/pgadmin4
```
Example:
```
$ docker run --name pgadmin_img -d -p 5050:5050 fenglc/pgadmin4
```

For making use of this postgresql-client find the IpAddress of this container and make use of it for port forwarding.

```
$  psql -U (userName) -h (postgresql-client_IpAddress) -p (PortOfPgAdmin)
```

Example:
```
$ psql -U docker -h 172.17.0.2 -p 5432
```

> NOTE: The Port `5432` is the default port number for postgreSQL using the command

The Docker PostgreSQL_client container IPAdress can be found using the command:
```
$ docker inspect (postgresql-client_containerName)
```

Example:
```
$ docker inspect pgadmin
```

This will render all the information about the cotainer in a JSON array.

![ContainerIpAddress](https://github.com/Dpurnima/myRepo/blob/master/containerIpAddress.PNG)

