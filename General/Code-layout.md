Piston code is split into four repositories. Piston uses maven for build automation/management. Each of these repositories except piston-master is also a maven module. piston-master repository is root maven parent project for all other maven modules. However I use flat maven mutli module project structure for piston-master instead of hierarchy project structure. For other modules, which are also maven parent projects, hierarchical structure has been used.

1. piston-master (this repository)
   This is master maven project.

2. [piston-core](http://github.com/koyadume/piston-core)
   This repository contains core piston code.

3. [piston-admin-apps](http://github.com/koyadume/piston-custom-apps)
   This repository contains administration apps for piston.

4. [piston-custom-apps](http://github.com/koyadume/piston-custom-apps)
   This repository contains custom apps for piston.

### Please note that master branch in all these repositories contains only one file (Apache License 2.0) and nothing else. So there is no use of master branch in all the above repositories.