### Mission statement 3.0

![Piston vs Portlet](images/portlet-vs-piston.png)

After working as a portal developer for past many years I felt that next in portal technology is due. Working on a leading portal server was very painful experience and I could never understand why some portals are so complex which makes implementing new ideas on these portal servers so difficult. It was difficult to digest how upgrading a portal takes months and not weeks or days or hours. 

If a company is spending a large part of development effort on upgrading the portals or getting their portal solutions work properly and efficiently then when it will get time to focus on implementing the business functionalities??

Piston is not a black box which you configure to get the desired result and where you are scared of looking or making changes into the code. It's a white box where you can look into the code with ease and see how its working internally. It's about keeping pace with evolving technologies. Today's technology landscape is much more complex than it was few years ago. Portals need to evolve at much faster pace in order to complement the technologies which are solving complex problems of present or which will solve complex problems of future.

You learn how annotation scanning works, a different way of using classloaders etc etc. Its an attempt to showcase how some challenges which developers face on day to day basis can be overcome using portal technology. At the same time its a tool which helps you to present and in turn consume or manipulate the information stored in different systems in an efficient way. 

I use Piston as an innovation platform for my ideas around Cloud computing, Big data and solutions to the problems which I face with the (personal or official) data present around me. Data is exploding not only in enterprise but in our personal and professional life too. You need a way to consume and find out relevant information from this (big) data so that you don't miss any crucial information which can help you to take better decisions. As a bonus you get the opportunity to solve some of the problems which people working on big data technologies are solving but other developers are not because they never got an opportunity to do so. Though you will solve these problems on a smaller scale, it will help you to prepare yourself for big problems up to a certain extent.

Piston is more about coding fun and very less about configuration. As a Java developer I never enjoyed configuring portals and I don't think any java developer does. 

I believe portal technology is like colors. Just like an artist can come up with amazing outcomes after mixing the colors on a canvas in different ways, how much portal technology can help you to innovate depends on how much innovative you can be with portals. This is same as an artist can produce amazing paintings with same colors but I can't.

## What is piston and how is different from other Java based portal servers?

Piston is a Java EE 7 based lean and pure servlet portal application framework which makes it very easy to develop portal applications. This is an attempt to find a pure servlet (no embedded container) solution for the problem called portal.

Piston is a action based framework. It's **heavily** inspired from struts framework.

Piston can be used to create hybrid (some pages are normal web pages while others are portal pages) or pure (all pages are portal pages) portal applications. Although piston can be used to develop web applications too, it's NOT recommended as there are already many good web applications frameworks out there for same purpose.

**One hour is all you need to become Piston expert even though you never developed a portal application.**

## Highlights

### Lean and pure servlet portal framework
Piston is a lean and pure servlet portal framework. In other words it does not embed portlet or any other container unlike other portal servers. I see following advantages with this approach -

* Servlet API is evolving at a much faster pace than portlet API. With pure servlet solution you can take full advantage of servlet API features.
* It's easy to keep pace with servlet API. Framework can be upgraded to a new version of servlet api in a very short time as soon as a new version of servlet API is available. It took me less than 2 days to upgrade this framework from Java EE 6 to Java EE 7.
* It's easy to debug the framework in case you encounter a bug or if a feature is poorly documented(These were two biggest pain points which I faced with a leading portal server as a portal developer).

### DevOps ready
Pison comes with a dedicated git repository, containing [Chef](https://www.getchef.com/) (an IT automation tool) based scripts, for installing all the dependencies (Java, Groovy, Maven, Ant, Tomcat, OpenDS and MySQL) of Piston. Install chef client, clone piston devops repo and execute a single command on a windows box. This is all you need to do in order to have all the required softwares for developing or running Piston in local windows development environment without any additional manual effort. No local development environment set up documents (for windows) anymore.

However documentation is also provided for those who want to set up local development environment manually for various reasons.

Following softwares can be installed in a windows environment using DevOps scripts  -
* Java
* Maven
* Ant
* Groovy
* Tomcat
* OpenDS
* MySQL


### Less but advanced features
Piston comes with less(core portal features) but advanced features required for creating portal applications. Here is a blog post explaining page layout designer of piston -
http://pistonportal.wordpress.com/2013/10/29/grid-designer

Creating pages and designing page layouts is the most important feature of any portal framework/server. Arranging data (which comes from different sources) on a portal page in such a way that you can convey maximum information to your portal users is much more important that merely aggregating the data. Piston page layout editor is where I have spent lot of time to make sure that a page layout of any complexity can be created right from the browser with no or minimal coding.

### Extend/modify framework with ease
Extend or modify the framework according to your needs and the technologies you like. E.g. I have used jQuery for Piston UI. You may modify it to use Dojo or any other javascript library of your choice.

### No dependency on application server
To run piston you only need a servlet container and not a full blown Java EE application server.

**Most of the web application frameworks come with their own tag libraries which are equivalent of jstl tag libraries. This makes life of a java developer difficult who work on multiple frameworks. In piston I have reused (ONLY) syntax of JSTL core tag library in order to avoid this inconvenience and to keep learning curve low.**

### Full automation (including complete code generation) is my ultimate target with Piston.