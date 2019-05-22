## About the frontend

[Dockerhub](https://hub.docker.com/r/patrickrng/php-sample-app/~/dockerfile/)

To test it, you need a database container, in this case, you can use mysql:5.7, you can get it [here](https://hub.docker.com/r/patrickrng/php-sample-app-backend/).  
Read more about it [here](https://github.com/PatrickRNG/php-sample-app/blob/master/backend/README.md)

### ***php Container***  
The frontend container, containing the php image  

***`docker-compose.yml` - php***

**`build`**: is the location of the Dockerfile in the ./frontend folder, that will build the image (php:7.2-apache).  
**`ports`**: Is the port that the php will run. PHP_PORT:CONTAINER_PORT  
**`env_file`**: The location of the `.env` file, to gain acess to the env variables, usually on the project root folder.  
**`links`** To be able to connect to the database, it depends on the `db` image, so here is where you link the php container, to the database container. Referencing the name of the database mysql container.  

---

### **Frontend Docker File**

`FROM php:7.2-apache` - Pulling the image php:7.2-apache from the Docker Hub.  

`RUN docker-php-ext-install mysqli` - Installing `mysqli` to connect to database.  

`WORKDIR /var/www/html` - Document Root, sets the working directory, for the `COPY` and other commands.  

`COPY . /var/www/html/` - Copying all the files from the current file, that got set in `WORKDIR`, to the Container directory */var/www/html/*.  
