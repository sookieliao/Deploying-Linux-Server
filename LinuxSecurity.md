## Intro to Linux Security
This section contains a number of security-related topics, including managing users, packages or the software installed on the server, various methods of authenticating users, how Linux manages file permissions and finally, how to configure a firewall.

#### The Rule of Least Pribilege 
A user or application only has enough permission to do its job, nothing extra.

### sudo v.s. su



### Updating Package Source List
  - Run `sudo apt-get update`
    This command will run through all repositories in `rtc/app/sources.list file and check what all sofewares are available and what those version numbers are. __This command doesn't actually perform any changes to the software__. It just make sure your system is aware of the latest information stored within all of these repositories that youo're making use of.

### Upgrading Packages
  - Run `sudo apt-get upgrade`
    This command will figure, list out all sofewares that needed to be updated, and ask "Do you want to continue?[y/n]". For fresh server, this is usually fine. But if you already have some applications up and running, you might wanna be more careful, test them in non-production environment, and make sure it's working fine before you make the changes to the production environment. Once you hit "yes", it'll download and installed all the new versions for the listed applicaations.