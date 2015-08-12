A frame represents common area across piston pages. In most situations a frame is responsible for rendering header, navigation and footer for a page. However you can put anything in a frame which is common across pages.

**XML is used as view definition language in piston.** This xml is actually kind of xhtml derived from html5 but should not be confused with xhtml5. You may think it as xml version of html5 with some extra tags. Also it adds some extra attributes to some html5 tags and vice versa.

**Please note a view in piston always generates html markup and not xhtml markup.**

Piston follows maven multi-module structure to keep the code separate for core, admin-apps and custom-apps modules. It is advised to follow the same approach to keep your code separate from piston modules. Since each of the piston modules have their own dedicated git repositories, its easy to update a module just by pulling latest code from corresponding git repository. You can create a maven module, which will be a module of piston-master root parent project like all other piston modules, to keep your custom code (frames, apps etc) separate from piston code. You can then have a git repository mapped to this newly created module.

Following is a basic example for creating a frame. For more details you can have a look at piston frames defined under piston-frames project of piston-core module.

Following are the steps for creating a new frame called 'frame1' -

**Steps**
* Make sure you have followed the steps described on [[this|Manual]] page to setup local development environment.

* Create a maven multi module project directly under piston workspace. After this, newly created module should be on the same level as piston-master. Lets call is custom-piston.
```
your_workspace
    piston-master
    custom-piston
```

* Create a maven web project under custom-piston. Lets call it custom-frames.

* Create a folder named 'frames' under src\main\webapp folder of custom-frames project.

* Create a folder named 'frame1' under frames folder. This is also the name of custom frame and will be used at a later stage. **Some names are reserved for piston frames and must not be used.**

* Create a xml file called 'frame.xml' under frame1 folder. 
```
your_workspace
    piston-master
    custom-piston
    	custom-frames
    		src
    			main
    				webapp
    					frames
    						frame1
    							frame.xml
```

* Add following code to frame.xml -

```xml
<?xml version="1.0" encoding="UTF-8"?>
<html 	xmlns="http://piston.koyad.in/html5" 
		xmlns:portal="http://piston.koyad.in/portal"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="http://piston.koyad.in/html5 ../xsd/html5.xsd http://piston.koyad.in/portal ../xsd/portal.xsd ">
	<head>
		<title>Frame1</title>
	</head>
	<body>
		<div>
			<!-- header -->
			<div id="header">
			</div>
			
			<!-- page content -->
			<div id="content">
				<portal:includePage />
			</div>
			
			<!-- footer -->
			<div id="footer">
			</div>
		</div>
	</body>
</html>
```

Above file is like any other xml file which uses tags from different schemas where each of these schemas has its own namespace. Details of piston tag libraries and all the tags available under these libraries can be found [[here|Piston tag libraries]].

Other things to note -

* 'html' should always be the root tag in frame.xml.
    
* 'http://piston.koyad.in/html5' is the namespace for piston html5 tag library.

* 'http://piston.koyad.in/portal' is the namespace for piston portal tag library.

* 'portal:includePage' is a special tag which is used to include markup for portal page in a frame.

Other than above points, frame.xml contains markup like any other html file provided the markup follows rules of xml.

**Referencing other types of artifacts (js, css etc) in frame.xml file -**

* To reference a javascript file called frame1.js in newly created frame, create a folder called js under frame1 folder and then create frame1.js under this folder. Now you can reference this js file in frame.xml using following code -

```html
<head>
	<title>Frame 1</title>
  	<script type="text/javascript" src="js/frame1.js"></script>
</head>
```


* To reference a css file called frame1.css in newly created frame, create a folder called css under frame1 folder and then create frame1.css under this folder. Now you can reference this css file in frame.xml using following code -

```html
<head>
	<title>Frame 1</title>
  	<link rel="stylesheet" href="css/frame1.css" />
</head>
```

* Add 'custom-frames' project as a dependency of piston-web project (Note : type should be 'war' and scope should be 'runtime')-

```xml
<dependency>
	<groupId>custom_frame_project_groupId</groupId>
	<artifactId>custom-frames</artifactId>
	<version>version</version>
	<type>war</type>
	<scope>runtime</scope>
</dependency>
```

* Now build piston-master project and make sure that newly created frame folder (frame1) reflects under 'frames' folder of piston war.

* Go to 'Manage Frames' page of Admin site and register new frame.

<img src="http://pistonportal.files.wordpress.com/2014/10/manage-frames1.png" />

Now you should be able to select newly created frame 'frame1' while creating/modifying a site.