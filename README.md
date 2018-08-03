# Demystifying Docker compose variables

I've concocted this project to alleviate the confusion that surround the use of environment variables with docker-compose files.

It's my attempt at clarifying things following the confusion in my head from those Docker issues:

* WARNING: The X variable is not set. Defaulting to a blank string. [#4189](https://github.com/docker/compose/issues/4189)
* Add support for `extends` feature in Compose v3 / docker stack deploy[#31101](https://github.com/moby/moby/issues/31101#issuecomment-301212524)


## Usage

```
$ docker-compose up test
$ docker-compose up prod
$ docker-compose up magic
$ FROM_CLI=wow docker-compose up magic
$ docker-compose up black-magic
$ docker-compose -f docker-compose.yml -f docker-compose.staging.yml up test
$ docker-compose -f docker-compose.yml -f docker-compose.staging.yml up prod
$ docker-compose -f docker-compose.yml -f docker-compose.staging.yml up magic
$ FROM_CLI=wow docker-compose -f docker-compose.yml -f docker-compose.staging.yml up magic
$ docker-compose -f docker-compose.yml -f docker-compose.staging.yml up black-magic
```

you can also run ``docker-compose config`` to display the compose-file with the in-container variables (specfied with **environment:** and **env_file:**) resolved.

you can also set the COMPOSE_FILE environment variable if you don't want to type all the compose file names:

```
$ export COMPOSE_FILE=docker-compose.yml:docker-compose.staging.yml
$ docker-compose up black-magic
```

to test the environment variables "inheritance" feature (to alleviate the disappearance of **extends**): 

```
$ docker-compose up queen-bee worker-bee sentinel-bee
```


## Requirement

it uses docker-compose format version 3.7 which requires Docker Engine 18.06.0+

Feel free to change the "version:" property in the **docker-compose.yml** to support older version or to explore behaviour with previous versions.
