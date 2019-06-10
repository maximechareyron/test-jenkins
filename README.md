#LIAM



## Set up the database

For development purposes, the database is hosted on a docker container. Here's how to set it up:
1. Install docker on your machine (Google is your friend)
2. Run `docker pull mysql/mysql-server:8.0` which will download the image of mysql server.
3. Start your container using `docker run --name=liam_mysql -d mysql/mysql-server:8.0`
4. You can check that your container is running using `docker ps`
5. A one-time password was generated. To get it, simply run `docker logs liam_mysql 2>&1 | grep GENERATED`
6. Connect to the database using `docker exec -it liam_mysql mysql -uroot -p` and then enter the password you just got.
7. update the password to a custom one using the following SQL request : `ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_new_password' `
8. Make sure the password you provided is properly filled in the `.env` file at the root of the project.
9. Get the IP of your docker container:
	* run `docker ps` to get the id of your container
	* then run `docker inspect <id> | grep ip` to get its ip
9. Make sure you can connect to the mysql server from the command line of your machine : `mysql -uroot -h <ip of the container> -P 3306 --protocol=tcp -p`
	* If you can't, it might be because the root user is not configured for your host machine.
	You will need to add the IP address of each system that you want to grant access to, and then grant privileges:
		```
		CREATE USER 'root'@'local_ip_address' IDENTIFIED BY 'some_pass';
		GRANT ALL PRIVILEGES ON *.* TO 'root'@'local_ip_address';
		```

