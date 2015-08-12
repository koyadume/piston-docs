Piston code is split into four repositories. Piston uses gradle for build automation/management. Each of these repositories except piston-master-gradle is also a gradle module. piston-master-gradle repository is root gradle project for all other gradle modules. However I use flat gradle mutli module project structure for piston-master-gradle instead of hierarchical project structure. For other modules hierarchical structure has been used.

1. piston-master-gradle (https://github.com/koyadume/piston-master-gradle)
   This is root gradle project.

2. [piston-core](https://github.com/koyadume/piston-core)
   This repository contains core piston code.

3. [piston-admin-apps](https://github.com/koyadume/piston-custom-apps)
   This repository contains administration apps for piston.