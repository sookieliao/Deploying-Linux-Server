# Deploying Linux Server
Deploying Linux Server Section from Udacity Fullstack Web Development course

## Intro to Linux

### Getting Started with Vagrant
In this course we’ll be working with Ubuntu. It’s an excellent distribution for a variety of use cases, including web servers. We’ll run our Ubuntu server within a virtual machine, which is a special piece of software running on your computer that acts as if it is a stand-alone computer.

To accomplish this requires a bit of setup but will give everyone the same Linux environment to work within, even if you’re on Windows or OSX currently.

### Required Software
If you've already downloaded and installed these items, perhaps while completing a different course, you do not need to download and install these items again.

  1. Download and install [VirtualBox](https://www.virtualbox.org/wiki/Download_Old_Builds_5_2). This is free software that will run the 
  virtual machine.
  2. Download and install [Vagrant](https://www.vagrantup.com/). This is an command line utility that makes it easy to manage and access 
  your virtual machines.
Note: Currently (July 2018), the version of VirtualBox you will want is 5.2. Newer versions do not yet support Vagrant.

### Course Environment
Follow these steps to setup an environment where you can work on this course:

  1. Create a new folder on your computer where you’ll store your work for this course, then open that folder within your terminal.
  2. Type `vagrant init ubuntu/trusty64` to tell Vagrant what kind of Linux virtual machine you would like to run.
  3. Type `vagrant up` to download and start running the virtual machine
This last step could take some time since the virtual machine files can be quite large. While you're waiting for it to download, feel free to continue with this course!

## Vagrant Commands
We’re now ready to get started working within our Linux virtual machine. If your download hasn’t completed from the initial setup, go ahead and take a break and come back when that has completed. You won’t be able to make further progress until the virtual machine is up and running as much of the course will take place within this environment.

Before we access our machine, let’s quickly review a few commands that vagrant provides to make managing your virtual machines much simpler. Remember, your vagrant machine lives within this specific folder on your computer so make sure you’re within that same folder your created earlier; otherwise these commands won’t work as expected.

  1. Type `vagrant status`
    This command will show you the current status of the virtual machine. It should currently read “default running (virtualbox)” along 
    with some other information.
  2. Type `vagrant suspend`
    This command suspends your virtual machine. All of your work is saved and the machine is put into a “sleep mode” of sorts. The 
    machines state is saved and it’s very quick to stop and start your work. You should use this command if you plan to just take a 
    short break from your work but don’t want to leave the virtual machine running.
  3. Type `vagrant up`
    This gets your virtual machine up and running again. Notice we didn’t have to redownload the virtual machine image, since it’s 
    already been downloaded.
  4. Type `vagrant ssh`
    This command will actually connect to and log you into your virtual machine. Once done you will see a few lines of text showing 
    various performance statistics of the virtual machine along with a new command line prompt that reads vagrant@vagrant-ubuntu-trusty-
    64:~$
    
Here are a few other important commands that we’ll discuss but you __do not__ need to practice at this time:

  1. `vagrant halt`
    This command halts your virtual machine. All of your work is saved and the machine is turned off - think of this as “turning the 
    power off”. It’s much slower to stop and start your virtual machine using this command, but it does free up all of your RAM once the 
    machine has been stopped. You should use this command if you plan to take an extended break from your work, like when you are done 
    for the day. The command vagrant up will turn your machine back on and you can continue your work.
  2. 'vagrant destroy'
    This command destroys your virtual machine. Your work is not saved, the machine is turned off and forgotten about for the most part. 
    Think of this as formatting the hard drive of a computer. You can always use vagrant up to relaunch the machine but you’ll be left 
    with the baseline Linux installation from the beginning of this course. You should not have to use this command at any time during 
    this course unless, at some point in time, you perform a task on the virtual machine that makes it completely inoperable.
