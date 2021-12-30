# Starting up the system

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

## Updating the build

From the command line, go to the project directory containing the **docker-compose.yml** file and enter command `docker-compose down` if `docker ps` shows the app is already running. Then, enter command `docker-compose build`. Then start it back up via `docker-compose up`.

## Accessing `psql` in a running container

The connection command will have the form
`\$ docker exec -ti NAME_OF_CONTAINER psql -U YOUR_POSTGRES_USERNAME NAME_OF_DB`