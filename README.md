# Deploying Linux Server
Deploying Linux Server Section from Udacity Fullstack Web Development course

### Connecting information
IP:54.244.185.77
URL:
SSH Port: 2200

### Software Installed
1. apache2 (sudo apt-get install apache2)
2. mod-wsgi (sudo apt-get install libapache2-mod-wsgi)
3. postgresql (sudo apt-get install postgresql)
4. pip (sudo apt install python-pip)

### Configuration Specification
1. Change ssh port from 22 to 2200
- sudo nano /etc/ssh/sshd_config
- change Port 22 to Port 2200
- restart: systemctl restart ssh

2. configure UFW firewall
- sudo ufw default deny incoming
- sudo ufw default allow outgoing
- sudo ufw allow tcp/2200
- sudo ufw allow www
- sudo ufw allow ntp
- sudo ufw enable
- (add tcp 2200 to AWS firewall as well)

3. Create new user "grader"
- sudo adduser grader

4. Give "grader" permission to sudo
- sudo nano /etc/sudoers.d/grader
- edit file "grader ALL=(ALL) NOPASSWD:ALL"

5. Add "ssh-key" for grader
(generate ssh key: ssh-keygen)
- switch to user "grader": sudo su -l grader
- add pub key to authorized keys
- mkdir .ssh
- sudo nano .ssh/authorized_keys
- add the pub key to this file, save and exit
- set permission: chmod 700 .ssh, chmod 644 .ssh/authorized keys

6. change localtimezone to UTC
sudo timedatectl set-timezone Etc/UTC

7. disable root accesss
- sudo nano /etc/ssh/sshd_config
- Edit "PermitRootLogin no"

8. make ".git" not publicly accessible
- sudo nano /etc/apache2/conf-enabled/security.config
- edit "<DirectoryMatch "/\.git">Require all denied </DirectoryWatch>

9. Deploy item catalog project
- Create catalogapp.wsgi file
- configure virtual host: sudo nano /etc/apache2/sites-available/000-default.conf
- sudo service apache restart


### Ohter 3-party Resources In this Application
- flask
- psycopg2
- requests
- SQLAlchemy
- oauth2client
- goolge-oauth2-tool
- Flask-HTTPAuth


