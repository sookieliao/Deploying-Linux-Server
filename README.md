# Deploying-Linux-Server
Deploying Linux Server Section from Udacity Fullstack Web Development course

## Intro-to-Linux

### Getting Started with Vagrant
In this course we’ll be working with Ubuntu. It’s an excellent distribution for a variety of use cases, including web servers. We’ll run our Ubuntu server within a virtual machine, which is a special piece of software running on your computer that acts as if it is a stand-alone computer.

To accomplish this requires a bit of setup but will give everyone the same Linux environment to work within, even if you’re on Windows or OSX currently.

### Required Software
If you've already downloaded and installed these items, perhaps while completing a different course, you do not need to download and install these items again.

1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Download_Old_Builds_5_2). This is free software that will run the virtual machine.
2. Download and install [Vagrant](https://www.vagrantup.com/). This is an command line utility that makes it easy to manage and access your virtual machines.
Note: Currently (July 2018), the version of VirtualBox you will want is 5.2. Newer versions do not yet support Vagrant.

### Course Environment
Follow these steps to setup an environment where you can work on this course:

1. Create a new folder on your computer where you’ll store your work for this course, then open that folder within your terminal.
2. Type `vagrant init ubuntu/trusty64` to tell Vagrant what kind of Linux virtual machine you would like to run.
3. Type `vagrant up` to download and start running the virtual machine
This last step could take some time since the virtual machine files can be quite large. While you're waiting for it to download, feel free to continue with this course!
