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

This will create a new Bash session in the container cont_postgresql.

Now, you are inside the container and can execute the postgreSQL commands. The following basic postgresql command helps in authenticating and login to the postgres

```
$ psql -U (Username) -h (docker_Container_IPAddress) -p (portNumber)
```

According to this Example:
```
$ psql -U docker -h 172.17.0.2 -p 5432
```

> NOTE: The Port `5432` is the default port number for postgreSQL using the command

The Docker container IPAdress can be found using the command:
```
$ docker inspect (containerName)
```

Example:
```
$ docker inspect cont_postgresql
```

This will render all the information about the cotainer in a JSON array.

![alt text](http://url/to/img.png)

## Testing the Database Created
As mentioned above, to make sure that a empty database named `docker` is created during the build using the username `docker` and password `docker`

