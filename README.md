# Data Warehouse

This project provides infrastructure for a personal data warehouse. It sets up a postGIS database, a pgadmin4 administration server, and an airflow server.

My main goal in this project is to have a sandbox to learn and experiment with different tools (namely docker and airflow), so all helpful feedback is welcome.

## Setup

To set up this infrastructure, first clone the repo and navigate into it

`$ git clone git@github.com:MattTriano/data_warehouse.git`
`$ cd data_warehouse`

then configure an `.env` file with the port numbers, usernames, and passwords you want for your system. For ease, you can just copy the example `.env` file 

`$ cp .env.example .env`

and then replace the placeholder values (the angle-bracketed parts) with your values.

You'll also have to create a `secrets` directory and files for your pgadmin4 username and password.  

`$ mkdir secrets`
`$ touch secrets/pgadmin_email.txt secrets/pgadmin_password.txt`

**Note**: 
*I'll probably simplify this later so that everything is just in the `.env` file. My first nontrivial personal project with Docker involved figuring out how to adapt the base pgadmin4 image to accept passwords as secrets rather than as environment variables (I assumed there was a lot more security to secrets than environment variables specified in a `.env` file, and now I know that it's not much more protection but a fair bit more complexity).*

## Starting up the system

From the project root dir, you can build the image via `$ docker-compose build`, then you can start up the containers via `$ docker-compose up -d` (`-d` detaches, so you can still have that terminal and you don't have to worry about accidentally shutting things down via ctrl+c).

## Accessing pgadmin4

Go to 0.0.0.0:5678 in a browser and log in.

### Connecting a db

You can create a new server by right-clicking **Servers** (in the tray on the left edge of the screen) -> **Create** -> **Server...**.

In the interface that pops up, 
1. On the **General** tab: enter any name (this is what you will see in the pgadmin4 interface) 
1. On the **Connection** tab:
	1. **Host name/address**: enter the service name for the database from the `docker-compose.yml` file
	1. **Port**: Use the port number from inside the container (not the port number for the host machine)
	1. **Username**: enter the database user name

Then click save. If things work, you should be good to go.

## Accessing the Airflow GUI

Go to 0.0.0.0:<AIRFLOW_WEBSERVER_PORT> in a browser and log in using the username and password you defined in the .env file.

## Accessing the Celery Flower Dashboard

Go to 0.0.0.0:<FLOWER_PORT> in a browser.

## Updating the build

From the command line, go to the project directory containing the **docker-compose.yml** file and enter command `docker-compose down` if `docker ps` shows the app is already running. Then, enter command `docker-compose build`. Then start it back up via `docker-compose up`.

## Accessing `psql` in a running container

The connection command will have the form
```{bash}
\$ docker exec -ti NAME_OF_CONTAINER psql -U YOUR_POSTGRES_USERNAME NAME_OF_DB
```

## Resources

### Airflow

* [Airflow concepts](https://airflow.apache.org/docs/apache-airflow/stable/concepts/overview.html)