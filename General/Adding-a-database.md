## App level changes
### Define a persistent unit in persistence.xml
```xml
<persistence-unit name="piston" transaction-type="RESOURCE_LOCAL">
	<provider>org.hibernate.ejb.HibernatePersistence</provider>
	<non-jta-data-source>java:comp/env/jdbc/authentication</non-jta-data-source>
	<properties>
		<property name="hibernate.dialect" value="org.hibernate.dialect.MySQL5InnoDBDialect" />
		<property name="hibernate.cache.use_second_level_cache" value="false" />
 		<property name="hibernate.cache.use_query_cache" value="false" />
 		
 		<property name="hibernate.show_sql" value="true" />
		<property name="hibernate.format_sql" value="true" />
	</properties>
</persistence-unit>
```

### Create an entry in context.xml (Make sure value of 'path' attribute matches target application context root) 
```xml
<Context antiJARLocking="true" path="/rest">
    <ResourceLink name="jdbc/authentication"
              global="jdbc/authentication"
              type="javax.sql.DataSource" />
</Context>
```

## Tomcat level changes
### Modify server.xml
```xml
<GlobalNamingResources>
    <Resource name="jdbc/authentication" type="javax.sql.DataSource" maxTotal="10" maxIdle="5" maxWaitMillis="10000" username="piston" password="piston" driverClassName="org.mariadb.jdbc.Driver" url="jdbc:mariadb://localhost:3307/authentication?relaxAutoCommit=true" />
</GlobalNamingResources>
```




