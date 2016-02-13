## App level changes
### Define a persistent unit in persistence.xml
```xml
<persistence-unit name="piston" transaction-type="RESOURCE_LOCAL">
	<provider>org.hibernate.ejb.HibernatePersistence</provider>
	<non-jta-data-source>java:comp/env/jdbc/piston</non-jta-data-source>
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
<Context path="/piston-service">
	<ResourceLink name="jdbc/piston" global="jdbc/piston" type="javax.sql.DataSource" />
	<JarScanner>
    	<JarScanFilter defaultTldScan="false" defaultPluggabilityScan="false" />
  	</JarScanner>
</Context>
```

### Initialize JPA EntityManagerFactory in servlet context listener
```
//Initialize JPA EntityManagerFactory
JPAEMFactory.initialize(Joiner.on(',').join(new String[] {
												DBConstants.PERSISTENT_UNIT_PISTON
											}));
```


## Tomcat level changes
### Modify server.xml
```xml
<GlobalNamingResources>
	<Resource name="jdbc/piston" type="javax.sql.DataSource" maxTotal="10" maxIdle="5" maxWaitMillis="10000" username="piston" password="piston" driverClassName="org.mariadb.jdbc.Driver" url="jdbc:mariadb://piston-db:3307/piston?relaxAutoCommit=true" />
</GlobalNamingResources>
```


