Piston follows maven multi-module structure to keep the code separate for core, admin-apps and custom-apps modules. It is advised to follow the same approach to keep your code separate from piston modules. Since each of the piston modules have their own dedicated git repositories, its easy to update a module just by pulling latest code from corresponding git repository. You can create a maven module, which will be a module of piston-master root parent project like all other piston modules, to keep your custom code (frames, apps etc) separate from piston code. You can then have a git repository mapped to this newly created module.

Following is a basic example for creating an app called 'custom-helloWorld' with a 'Hello World' plugin.

**Steps -**

* Make sure you have followed the steps described on [[this|Manual]] page to setup local development environment.
* Create a maven multi module project directly under piston workspace. After this, newly created module should be on the same level as piston-master. Lets call is custom-piston.
```
your_workspace
    piston-master
    custom-piston
```

* Create a maven web project under custom-piston. Lets call it custom-helloWorld. 
```
your_workspace
    piston-master
    custom-piston
    	custom-helloWorld
```

Make sure pom.xml file of custom-helloWorld looks as following -
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>in.koyad.piston.apps</groupId>
	<artifactId>custom-helloWorld</artifactId>
	<version>1.0-SNAPSHOT</version>
	<packaging>war</packaging>

	<build>
		<plugins>
			<plugin>
				<artifactId>maven-compiler-plugin</artifactId>
				<configuration>
					<source>1.8</source>
					<target>1.8</target>
				</configuration>
			</plugin>
			<plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <configuration>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                    <appendAssemblyId>false</appendAssemblyId>
                    <archive>
				      	<manifestEntries>
							<App-Name>HelloWorld</App-Name>
							<App-Title>HelloWorld</App-Title>
							<Res-Folder>helloWorld</Res-Folder>
						</manifestEntries>
					</archive>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
			<plugin>
				<artifactId>maven-war-plugin</artifactId>
				<configuration>
					<packagingExcludes>WEB-INF/</packagingExcludes>
					<failOnMissingWebXml>false</failOnMissingWebXml>
				</configuration>
			</plugin>
			
		</plugins>
	</build>

	<dependencies>
		<!-- Internal -->
		<dependency>
			<groupId>in.koyad.piston</groupId>
			<artifactId>piston-common</artifactId>
			<version>1.0-SNAPSHOT</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>in.koyad.piston</groupId>
			<artifactId>piston-ui</artifactId>
			<version>1.0-SNAPSHOT</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>in.koyad.piston</groupId>
			<artifactId>piston-service-delegate</artifactId>
			<version>1.0-SNAPSHOT</version>
			<scope>provided</scope>
		</dependency>
		
		<!-- Third party -->
		<dependency>
			<groupId>javax</groupId>
			<artifactId>javaee-web-api</artifactId>
			<version>7.0</version>
			<scope>provided</scope>
		</dependency>
	</dependencies>

</project>
```

- Value of 'App-Name' manifest entry is used while placing a plugin on a page. So it should be kept constant throughout the life of an app. Any change in the value of this parameter will require updating the app name on all the pages which are using plugins from this app.
- Value of 'App-Name' manifest entry is used to display the app title on page layout designer.
- Value of 'Res-Folder' manifest entry is the name of folder under piston web application where the static artifacts of this app are copied during build. 


### Create a new class 'HelloWorldPlugin' which extends 'Plugin' class -

```java
package in.koyad.piston.app.helloWorld.plugins;

import in.koyad.piston.app.helloWorld.actions.HelloWorldPluginAction;
import in.koyad.piston.common.utils.LogUtil;
import in.koyad.piston.controller.plugin.Plugin;
import in.koyad.piston.controller.plugin.annotations.AnnoPlugin;
import in.koyad.piston.controller.plugin.annotations.AnnoPreference;

@AnnoPlugin(name = "helloWorld", title = "Hello World", 
	defaultAction = HelloWorldPluginAction.ACTION_NAME
)
public class HelloWorldPlugin extends Plugin {

	private static final LogUtil LOGGER = LogUtil.getLogger(HelloWorldPlugin.class);
	
	@Override
	public void preProcess() {
		LOGGER.enterMethod("preProcess");
	}
	
	@Override
	public void postProcess() {
		LOGGER.exitMethod("postProcess");
	}
	
}
```

* HelloWorldPlugin class extends Plugin class which is base class for all the plugin classes.
* 'name' defines the name of plugin class. This should be kept constant throughout the life of plugin as this is referenced in portal page markup when this plugin is placed on a portal page. Any change in the value will require updating plugin name on all the portal pages which are using this plugin.
* 'title' attribute defines the title of plugin. This is used on **Apps** panel of page layout designer.
* 'defaultAction' defines the action which a plugin will invoke if an action has not been passed to plugin class.
* preProcess() and postProcess are plugin lifecycle methods which are invoked before and after process() method of plugin respectively. 



### Create a new class 'HelloWorldPluginAction' which extends 'PluginAction' class -

```java
package in.koyad.piston.app.helloWorld.actions

import in.koyad.piston.common.exceptions.FrameworkException;
import in.koyad.piston.controller.plugin.PluginAction;
import in.koyad.piston.ui.utils.PistonContextUtil;

public class HelloWorldPluginAction extends PluginAction {

	@Override
	protected String execute() throws FrameworkException {
		PistonContextUtil.setRequestAttribute("msg", "Hello World!!");
		return "/pages/helloWorld.xml";
	}

}
```

* HelloWorldPluginAction class extends PluginAction class which is base class for all plugin action classes.
* A plugin action should provide implementation for execute() method from PluginAction class.


* Create a folder named 'pages' under webapp folder and create a xml file named 'helloWorld.xml' under this folder.

### Add following code to helloWorld.xml file -

```xml
<plugin:page 
	xmlns="http://piston.koyad.in/html5" 
	xmlns:plugin="http://piston.koyad.in/plugin"
	xmlns:c="http://piston.koyad.in/core" 
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://piston.koyad.in/html5 http://piston.koyad.in/html5 
						http://piston.koyad.in/plugin http://piston.koyad.in/plugin 
						http://piston.koyad.in/core http://piston.koyad.in/core">
	<plugin:body>
		<c:out value="${msg}" />
	</plugin:body>
</plugin:page>
```

* 'plugin:page' should be root tag of all plugin pages. It's like html tag for plugin pages.
* 'plugin:body' is one of the two children (another is plugin:head) of plugin:page tag. It's like html body tag for plugin pages.


### Register app with piston-web project
* Add following code under **maven-dependency-plugin** in pom.xml file of piston-web project
```xml
<artifactItem>
    <groupId>in.koyad.piston.apps</groupId>
    <artifactId>custom-helloWorld</artifactId>
    <version>1.0-SNAPSHOT</version>
    <overWrite>false</overWrite>
    <outputDirectory>${project.build.directory}/${project.build.finalName}/WEB-INF/${appLibs}</outputDirectory>
</artifactItem>
```

* Add following code under **maven-war-plugin** in pom.xml file of piston-web project
```xml
<overlay>
    <groupId>in.koyad.piston.apps</groupId>
    <artifactId>custom-helloWorld</artifactId>
    <targetPath>${appResources}\helloWorld</targetPath>
</overlay>
``` 
Please note that last part of 'targetPath' must be value of 'Res-Folder' manifest entry in pom.xml of app project.

* Add following code under **dependencies** tag of pom.xml file of piston-web project
```xml
<dependency>
    <groupId>in.koyad.piston.apps</groupId>
    <artifactId>custom-helloWorld</artifactId>
    <version>1.0-SNAPSHOT</version>
    <type>war</type>
    <scope>runtime</scope>
</dependency>
```


* Now go to piston-master project and issue **mvn clean install** to build piston web application. After this newly created app will be visible under **Manage Apps** page of Admin site.