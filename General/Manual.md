* Clone piston git repositories in your local workspace.

	* Create a folder at a location of your choice. This will be referred as piston workspace in rest of the document.

	* Clone 1.0 branches of following repositories in piston workspace -

		http://github.com/koyadume/piston-master

		http://github.com/koyadume/piston-core

		http://github.com/koyadume/piston-admin-apps

		http://github.com/koyadume/piston-custom-apps

* Make sure JDK 1.8 (or higher) and Maven 3.x (or higher) are installed.

* Set-up ldap server 

	* Install a ldap server (I use OpenDS with piston) using instructions available on internet.

	* Import required users and groups/roles in your ldap server using follwing ldif file -

	https://github.com/koyadume/piston-share/blob/master/ldap/piston.ldif

	Above file with add following nodes to ldap server -

	o = koyad.in
	
	---- ou = piston
	
	-------- ou = users
	
	------------ uid = pistonAdmin (Piston admin user, password is same as uid)
	
	------------ uid = piston (Piston normal user, password is same as uid)
	
	------------ uid = tomcat (tomcat admin user, password is same as uid)
	
	-------- ou = groups
	
	------------ cn = pistonAdmins (Piston admin group)
	
	-------- ou = roles
	
	------------ cn = manager-gui (Tomcat gui manager role)
	
	------------ cn = manager-jmx (Piston jmx manager role)


* Set-up mysql server 

	* Install MySQL Community server v5.6/5.7 using instructions available on internet.
	
	* Clone 1.0 branch of http://github.com/koyadume/piston-sql repository to piston workspace.
	
	* Execute following command from piston-sql\create folder to create piston database with all the tables required for piston -
	
	mysql -u root -p < CREATE_TBL_ALL.sql
	
	* Execute following command from piston-sql\insert folder to insert initial piston data -
	
	mysql -u root -p < INSERT_TBL_ALL.sql
	
	
* Set-up tomcat

	* Download tomcat 8.0.x from internet and install it to a location of your choice.
	
	* Make following changes in conf/server.xml file under tomcat root directory -
	
		* Comment out following line -
		
		```
		<Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
       ```

       * Add following resource under &lt;GlobalNamingResource&gt; -

       ```
       <Resource name="jdbc/pistonDB" global="jdbc/pistonDB" auth="Container" type="javax.sql.DataSource" maxTotal="50" maxIdle="10" maxWaitMillis="10000" username="root" password="piston" driverClassName="com.mysql.jdbc.Driver" url="jdbc:mysql://localhost:3306/piston?relaxAutoCommit=true" />
       ```
              
      * Replace following line - 
      
      ```
      <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      ```        
      
      with this line -
      
      ```
      <Realm className="org.apache.catalina.realm.JNDIRealm"
				connectionURL="ldap://localhost:389" userPattern="uid={0},ou=users,ou=piston,o=koyad.in" 
                  roleBase="ou=roles,ou=piston,o=koyad.in" roleName="cn" roleSearch="(uniqueMember={0})" />
          
		```
		
* Deploy piston on tomcat

	* Go to piston-master folder and execute following command -
	
	mvn clean install
	
	Above command will only work if you have JAVA_HOME (pointing to JDK 1.8 or higher) and CATALINA_HOME (pointing to your tomcat root directory) environment variables defined.
	
* Open a browser windows and navigate to 'http://localhost:8080/piston/web/loginScreen' to access login screen of piston.

* Enter piston admin credentials (username : portalAdmin, password : portalAdmin). 

* In order to access a page under another site, you should use following url -

http://localhost:8080/piston/portal/site-&lt;site_mapping&gt;/&lt;page_mapping&gt;

Where -

	site_mapping is mapping for a site
	page_mapping is mapping for a page
	
For example - If you create a site called 'Demo' with mapping 'demo' and a page directly under this site with mapping 'page1', then the url for this page will be http://localhost:8080/piston/portal/site-demo/page1