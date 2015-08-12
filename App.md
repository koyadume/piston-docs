An app in piston is a mini web application which provides content, rendered by tiles on a portal page, through plugins.

On the other hand an app is a collection of Plugins and Plugin actions. A plugin acts as a front controller which executes one or more plugin actions during a request. A plugin is similar to ActionServlet of Struts 1 framework with two major differences -
* There is NO similarity between Plugin lifecycle and Servlet life cycle.
* There can be one or more plugins in an app.

Each app is loaded by a separate classloader which is also child of the classloader which loads portal application. 

On the code level an app project layout is same as a maven web project but without any WEB-INF folder. During build, a jar containing class files of app and a war containing static resource of app are generated. Further in build process app jar is copied to a special folder (other than WEB-INF\lib and defined in pom.xml of app) of piston application. Also static resources of app are merged with piston application after copying these to a special folder as defined in pom.xml of app. Following picture explains the same -

<p>
   <img src="http://pistonportal.files.wordpress.com/2014/10/app-piston-merge1.png?w=595" />
</p>