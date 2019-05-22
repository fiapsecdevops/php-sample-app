## About the backend

### ***db Container***
The backend container, containing the mysql image  

`docker-compose.yml` - db

**`build`**: is the location of the Dockerfile in the ./backend folder, that will build the image (mysql:5.2).  
**`ports`**: Is the port that Mysql will run. MYSQL_PORT:CONTAINER_PORT  
**`volumes`**: Is used to transform the backend, from stateless to stateful, storing the data, meaning that it wiil not lose the data.  
**`environment`**: Here is where you set the Environment variables for the mysql image.  
**`env_file`**: The location of the `.env` file, to gain acess to the env variables, usually on the project root folder.

---

### **Backend Docker file**

`FROM mysql:5.7` - Pulling the mysql:5.7 image from Docker Hub.  
`COPY ./demo.sql /docker-entrypoint-initdb.d` - Copying the *demo.sql* file, to the `/docker-entrypoint-initdb.d`, is directory is used as a start point to populate database (In this case using demo.sql);
