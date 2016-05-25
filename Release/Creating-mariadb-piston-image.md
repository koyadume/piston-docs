* ```mariadb-piston``` contains piston db installed on top of MariaDB. These images are stored in ```koyadume/mariadb-piston``` repository on dockerhub. 

* Create a container using koyadume/docker-mariadb image -
```
docker run -d -p 3307:3306 --name=mariadb koyadume/docker-mariadb:dockerhub-10.0.22
```

* Login to container and then login to mysql -
```
docker exec -it <container_id> bash
export TERM=dumb
mysql -u root -p
Enter 'secret' as password.
```

* Execute following sql statements -
```sql
CREATE USER 'piston'@'%' IDENTIFIED BY 'piston';

SET @@SQL_MODE = CONCAT(@@SQL_MODE, ',NO_AUTO_CREATE_USER');
GRANT ALL PRIVILEGES ON piston.* TO 'piston'@'%';
GRANT ALL PRIVILEGES ON steam.* TO 'piston'@'%';
GRANT ALL PRIVILEGES ON userMgmt.* TO 'piston'@'%';
GRANT ALL PRIVILEGES ON turbine.* TO 'piston'@'%';

FLUSH PRIVILEGES;
```

* Now connect to this container from HeidiSQL using following information to validate that container can be accessed from remote location -
```
Host - Docker host
user - piston
password - piston
port - 3307
```

* Execute following script from ```piston-setup\scripts``` folder after adjusting docker host name in this script -
```
setupPistonDBDocker.bat piston piston
```

* Commit changes to container -
```
docker commit <container_id> koyadume/mariadb-piston:dockerhub
```

* Create a container using newly created image ```koyadume/mariadb-piston``` image -
```
docker run -d -p 3307:3306 --name=mariadb-piston koyadume/mariadb-piston:dockerhub-core-2.3-turbine-1.0
```

* Now connect to this container from HeidiSQL using following information to validate that container can be accessed from remote location -
```
Host - Docker host
user - piston
password - piston
port - 3307
```

* Push newly created image
```
docker push koyadume/mariadb-piston:dockerhub-core-2.3-turbine-1.0
```



