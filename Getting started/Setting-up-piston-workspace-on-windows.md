## Create folder structure
Create a folder `git-repos` at a location of your choice with following structure -
```
git-repos
	devops
    piston
        apps
    piston-ext
    	apps
    	frames
```

## Clone piston-deploy-workspace repository
```
cd git-repos\devops
git clone https://github.com/pistonPortal/piston-deploy-workspace.git
```

## Install various runtimes/tools required by Piston
### Java
* Install latest version of `Oracle JDK 8` from internet.
* Adjust value of `JAVA_HOME` environment variable in `piston-deploy-workspace\scripts\setenv.bat` file and point it to JDK installation root directory.

### Ant
* Install latest version of `Ant`.
* Adjust value of `ANT_HOME` environment variable in `piston-deploy-workspace\scripts\setenv.bat` file and point it to Ant installation root directory.
* Create a folder `ext` under ant installation directory.
* Copy `https://bitbucket.org/bbshailendra/piston-ant/downloads/piston-ant-1.0.2.jar` to newly created folder.

### Gradle 
* Install latest version of Gradle.
* Adjust value of `GRADLE_HOME` environment variable in `piston-deploy-workspace\scripts\setenv.bat` file and point it to Gradle installation root directory.

### Tomcat
* Install latest version of `Tomcat`.
* Adjust value of `CATALINA_BASE` environment variable in `piston-deploy-workspace\scripts\setenv.bat` file and point it to Tomcat installation root directory.
* Download `mariadb-java-client-1.5.2.jar` from internet and copy it to `<tomcat_installation_directory>\lib` folder.
* Edit `<tomcat_installation_directory>\conf\server.xml` file and make sure that content of `<GlobalNamingResources>` and `<Realm>` tags are as following -
```xml
<GlobalNamingResources>
    <!-- Editable user database that can also be used by
         UserDatabaseRealm to authenticate users
    -->
	<!--
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
	-->
	<Resource name="jdbc/piston" type="javax.sql.DataSource" maxTotal="10" maxIdle="5" maxWaitMillis="10000" username="piston" password="piston" driverClassName="org.mariadb.jdbc.Driver" url="jdbc:mariadb://piston-db:3306/piston?relaxAutoCommit=true" />
    <Resource name="jdbc/steam" type="javax.sql.DataSource" maxTotal="10" maxIdle="5" maxWaitMillis="10000" username="piston" password="piston" driverClassName="org.mariadb.jdbc.Driver" url="jdbc:mariadb://piston-db:3306/steam?relaxAutoCommit=true" />
    <Resource name="jdbc/userMgmt" type="javax.sql.DataSource" maxTotal="10" maxIdle="5" maxWaitMillis="10000" username="piston" password="piston" driverClassName="org.mariadb.jdbc.Driver" url="jdbc:mariadb://piston-db:3306/userMgmt?relaxAutoCommit=true" />
</GlobalNamingResources>
```

```xml
<Realm className="org.apache.catalina.realm.LockOutRealm">
    <!-- This Realm uses the UserDatabase configured in the global JNDI
         resources under the key "UserDatabase".  Any edits
         that are performed against this UserDatabase are immediately
         available for use by the Realm.  
    <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
           resourceName="UserDatabase"/> -->
	<Realm className="org.apache.catalina.realm.DataSourceRealm" dataSourceName="jdbc/userMgmt" userTable="user" userNameCol="uid" userCredCol="password" userRoleTable="user_role" roleNameCol="role_name" />
</Realm>
```

### MariaDB
* Install latest version of `MariaDB 10.1.x`.
* Define an environment variable `MARIADB_HOME`. Value of this variable should be mariadb installation root directory.
* Append `%MARIADB%\bin` to `Path` environment variable.
* Create an entry into windows `C:\Windows\System32\drivers\etc\hosts` file as following -
```
<mariadb_server_ip_address> piston-db
```
* Go to `piston-deploy-workspace\properties` folder and adjust value of `mariadb-port` and `mariadb-pwd` properties in `mariadb.properties` file according to your environment.


## Clone git repositories
```
cd git-repos\piston
git clone -b 2.x https://github.com/pistonportal/piston-core.git

cd git-repos\piston\apps
git clone -b 1.x https://github.com/pistonportal/admin-appsMgmt.git
git clone -b 1.x https://github.com/pistonportal/admin-siteExplorer.git
git clone -b 1.x https://github.com/pistonportal/admin-steam.git

cd git-repos\piston-ext\apps
git clone -b 1.x https://github.com/pistonportal/custom-userMgmt.git
```

## Deploy code on local tomcat server as well as create various DBs and tables **(Make sure MariaDB is running)** - 
```
cd git-repos\devops\piston-deploy-workspace\scripts
setupPistonFromLocalWorkspace.bat
```
**Note - Use following command in order to deploy piston and apps code without creating DBs and tables**
```
setupPistonFromLocalWorkspace.bat skipDBs
``` 

## Testing
Assuming tomcat is listening on 8080 port, enter following url in browser to initialize Piston -
```
http://localhost:8080/piston/web/scanAndRegisterApps
```

Use following url to access `admin` site -
```
http://localhost:8080/piston/portal/site-admin/appAdmin
```

Enter `portalAdmin` for both username and password on login screen to proceed.


## Eclipse setup
* Go to `git-repos\piston\piston-core` folder and execute following commands -
```
gradle cleanEclipse eclipse
gradle clean install
```
 
* Go to `git-repos\piston\piston-apps` folder and execute following command from every folder under this folder -
```
gradle cleanEclipse eclipse
```

* Go to `git` perspective in eclipse and import all git repositories under `git-repos\piston` folder.
* Lombok setup
	- Download latest version of lombak.
	- Execute following command from the folder where lombok was downloaded -
```
java -jar lombok-x.y.z.jar
```
	- Select `eclipse.exe` file for your local eclipse installation to configure eclipse with lombok.
 
