---
title: Code Deployment
---

# Code Deployment

We use the familiar and popular [git][git] version control tool to push your code changes to a remote repository on our build servers. Each resin.io application has a unique remote repository associated to it and all code changes on the `master` branch of this repository will be built and delivered to your device fleet. When our servers receive your changes on `master` a chain reaction is set in motion in which your code is built for the specified target architecture, bundled into a [Docker container][docker] and then systematically rolled out to your fleet of devices in the field.

__Note:__ The resin.io git repository is not intended as a code hosting solution, and we cannot guarantee the persistence of data in resin.io git remotes.

![how deployment works](/img/common/how_deploy_works.jpg)

# Building Containers

The method our builders use to build your code depends on the project you are pushing. If your project includes a Dockerfile, the builders will execute every command in the Dockerfile, from including the base OS you define, to installing packages, pulling git repositories, and running any other commands you specify.

Alternatively, if your project includes a package.json (i.e. a node.js project), then that will be used instead to create an implicit Dockerfile, which simulates the build process a node.js/npm project expects. In this way, we are able to transparently run node.js projects on resin.io, while taking advantage of some of Docker’s caching features.

A Dockerfile will always give you more power to fine-tune the build process, but it’s also good to start fast without one, since you can shift to a Dockerfile whenever you like. We will soon add more languages to the “first-class” support we give to node.js. Until then, any other language can be used by adding a Dockerfile. It’s important to note that the environment within which your code gets built will match the devices you use for your app. So if you’re for example pushing to an app containing BeagleBone Black devices, we’ll build your code in an ARMv7 environment, while for the Raspberry Pi B+ it would be ARMv6.

Now that you have a better view of the build and deployment process, you may want to read about how the resin.io device OS is composed and [what is installed on a device](/understanding/understanding-devices).


[docker]:https://www.docker.com/
[git]:http://git-scm.com/
