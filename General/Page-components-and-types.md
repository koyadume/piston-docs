A page in piston is made of three components -

**Frame**

A frame represents common area across piston pages. Frame is responsible for rendering header, navigation and footer for a page.

**Grid**

A grid represents layout of a portal page.

**Tiles**

Tiles are small windows on a page which display content provided by plugins. A tile gets it content from a plugin which is a part of an app. A plugin invokes an action from all the available actions in the app to get the data for the tile.

![Page components](http://pistonportal.files.wordpress.com/2014/09/page-components1.png?w=550&h=315)

Piston uses xml as view definition language. Following types of pages can be created in piston -

* **Normal**

In this type of piston pages markup for grid and markup to include tiles are stored together as a single xml file.

* **Synchronous**

I realized the need of this type of portal page when I started working on solving docker problem with piston. A normal portal page in piston fires plugins in random order which is not suitable for solving problems like docker where creation of a dependent image requires that its dependency should be in place. In this type of page, plugins are fired in a particular manner and the execution of a plugin depends on the successful execution of another plugin which this plugin depends on. Its like (logically) arranging plugins in a tree like dependency structure where a child plugin will be executed only if its parent plugin is executed successfully.

![Bolt](images/piston-docker-cloud.png)

* **Grid** (Not implemented yet)

Sometimes it is desired to control page layout for a group of pages from a central location. In piston this is achieved through grid pages. A grid page shares its page layout with other grid pages. In this type of pages, page layout is stored separately while association between tile containers (grid blocks) and tiles is stored in a table. While creating a grid page, a layout is selected from a collection of layouts instead of creating it through grid designer.

* **Explicit** (Not implemented yet)

Although it is possible to create complex layouts using grid designer, there may be some situations where desired layout can’t be created using grid designer. As piston pages are xml files, these xml files can be created manually and uploaded to piston to create pages.