Piston comes with a dedicated repository (devops-piston-windows) which contains DevOps(Chef based) scripts for installing all the dependencies of piston on a **windows box**. All you need to do is install Chef client from http://www.getchef.com and then run a single command to install/configure following softwares on your windows box -

* Java
* Groovy
* Maven
* Ant
* Tomcat
* OpenDS
* MySQL

### How to use these scripts

* Install latest version of chef client for windows from http://www.getchef.com.
* Clone [devops-piston-windows](https://github.com/koyadume/devops-piston-windows) to a location of your choice on your windows box.

* Clone following cookbooks from 'https://github.com/opscode-cookbooks' to devops-piston-windows\cookbooks folder -

    * chef_handler
    * windows

* Go to devops-piston-windows directory and issue following command -
```
chef-solo -c .chef\solo.rb -j .chef\node.json
```

Only missing piece here for setting up complete local development environment is installing/configuring eclipse. This will be available soon.