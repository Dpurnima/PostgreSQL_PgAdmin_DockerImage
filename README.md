# Docker Image for PostgreSQL and PgAdmim

You can create your own Docker image by using `Dockerfile` if there is no Docker image in [Docker Hub](https://hub.docker.com/) that suites your need.

## Dockerfile For PostgreSQL

The Dockerfile given creates the postgreSQL image by copying the License key and PostgreSQL respository for installing it. And it also creates a `User` with `Password` inside which creates an Empty Database which could help us in future steps.

For Building this Dockerfile in command Prompt use the below given command:

```
$ docker build -t (imageName) .
```
Example:

    $ docker build -t img_postgresql .
    
Here, Option -t is used to name the image ascontentserverimage, image name should always be in lowercase alphabets and should not contain anyspaces . This command could create a Docker image named `img_postgresql`.

You can check the image created using command 
    `$ docker images`

To Run this image:

```
$ docker run -it --name (containerName) (postgresQL_imageName)
```
Example:

    $ docker run -it --name cnt_postgresql img_postgresql
    
This will successfully create the PostgreSQL container named `cnt_postgresql`. The Option '--name' is used to give the proper name to container which should not have any spaces between and the -Flag '-it' is used to  run container interactively and attached to your terminal.

Now, using the command `$ docker ps` you could see the container created in the name given (say cnt_postgresql).

## Testing the Database created
As mentioned above, to make sure that a empty database named `docker` is created during the build using the username `docker` and password `docker`

