## Intro to Linux Security
This section contains a number of security-related topics, including managing users, packages or the software installed on the server, various methods of authenticating users, how Linux manages file permissions and finally, how to configure a firewall.

#### The Rule of Least Pribilege 
A user or application only has enough permission to do its job, nothing extra.

#### sudo v.s. su

### Apt-get

#### Run `man aot-get`
  - This command will list out all operations you can do with apt-get.
  
#### Updating Package Source List
  - Run `sudo apt-get update`
    This command will run through all repositories in `rtc/app/sources.list` file and check what all sofewares are available and what those version numbers are. __This command doesn't actually perform any changes to the software__. It just make sure your system is aware of the latest information stored within all of these repositories that youo're making use of.

#### Upgrading Packages
  - Run `sudo apt-get upgrade`
    This command will figure, list out all sofewares that needed to be updated, and ask "Do you want to continue?[y/n]". For fresh server, this is usually fine. But if you already have some applications up and running, you might wanna be more careful, test them in non-production environment, and make sure it's working fine before you make the changes to the production environment. Once you hit "yes", it'll download and installed all the new versions for the listed applicaations.
    
#### Removing unused packages
  - Run `sudo apt-get autoremove`
    This command will run through all packages and remove unused ones.
    
### Managing Users

#### Run `sudo adduser userName`
  This will create a user with username **userName** After entering passwords, some questions will pop up, those are optional.
  ![Create user.](/createUser.png)
  
  Then we can login in as newly created user by running `ssh newUserName@127.0.0.1 -p 2222`
  (the `vagrant ssh` is actually just a shortcut for this command.)
  - __SSH__ is the application we use to remotely connect to the server
  - __127.0.0.1__ is the IP address we wanna connect to, which is a standard IP address for localhost or the same computer I'm currently on
  - __newUserName@__ specifies the user we wanna login as
  - __-p 2222__ flag tells us to connect using port 2222, so when vagrant sets up our virtual machine, it automatically sets up this port locally, and forwards it to the virtual machine. 
  ![Login in as new user.](/login.png)

### Giving Sudo Access
  since newly created usuer probably doesn't belong to the administration group, he/she won't be able to perform the administrative operations. To fix this, we'll grant the new user with the right to do sudo!
  - First of all, let's run `/etc/sudoers` to check who has right to do sudo operations.
    We can see root and admin beling listed in the file.
    ![](/sudo.png)
    For some distribution server, we can directly modify here and insert the new username as the rest. But it's a bit different for Ubuntu. At the bottom from the previous image, there's this line `#includedir /etc/sudoers.d`, which makes the server includes users in __sudoers.d__ as if they were written directly in sudoders file. This is common pattern, since distribution updates could over the sudoers file. And if that were happen, we could lose all users added here. By keeping the customization in the other directory, they system elimicates that risk.
  - Let's add our new user into sudoers.d file by creating a copy of an existing one, say, vagrant, here's the command 
    `sudo cp /etc/sudoers.d/vagrant /etc/sudoers.d/newUserName`.
  - Then let's edit the /`/etc/sudoers.d/newUserName` file by changing "__vagrant__ ALL=(ALL) NOPASSWD:ALL" to "__newUserName__ ALL=(ALL) NOPASSWD:ALL", and save it.
  - Just to mention, we can force a user to change the password by running `sudo passwd -e username`, which will set the username's password to expired.
  
### Key Based Authentication
Instead of relying on passwords, key-based authentication replies on physical files located on the server and your personal machine - the one you're logging in from.
#### Basic Concept 
  1. The server will generate a random message and send to the client.
  2. After receiving the message, the client will encrypt the message with their __private key__. And send that encrypted message back to the server.
  3. After receiving the encrypted message, the server will decrypt this message with their __public key__, and if the decrypted message equals the value they sent, the client is authenticated.
![](/keyBasedAuth.png)
#### Implementation
  1. Generating the key pairs in our **local**, remember, ***you never wanna share your private jey with ANYONE ELSE!*** We can do this by running `ssh-keygen`. After executing the command, two files will be generated, theidentification and the public key (.pub), and the .pub file is the one we're gonna place in the server to perform key-based authentication.
  
  2. To place the public key on the server, we must first login as the user we wanna perform key-based authentication. 
  
  3. Once logged in, create a **.ssh** directory, where all our key related files must be stored, by `mkdir .ssh`.
  
  4. Then create another file within this directory called authorized_keys, which will store all of the public keys that **this account** is allowed to use for authentication, with one key per line in that file. We do this by running command `touch .ssh/authorized_keys`.  ([What's Touch](https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/))
  
  5. Back to local machine, read out the contents in the .pub file with command `cat .ssh/filename.pub`, copy them.
  
  6. Back to server, edit the authorized_keys file by `nano .ssh/authorized_keys`, paste in the contents, and save it. 
  
  7. Last step, we need to set up specific permissions for this user by running these commands :`chmod 700 .ssh` and `chmod 644 .ssh/authorized_keys`.
  
  8. It's done! We can then try to log in to the server as the new user, but instead of using passwords, we now do `ssh newUserName@127.0.0.1 -p 2222 -i ~/.ssh/keyPairIdentificationFile`.
