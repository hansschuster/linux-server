# Linux Server Project

Installation and configuration of a Linux server as part of Udacity's
Full Stack Web Developer Nanodegree. Deployment of earlier project
[item catalog app](https://github.com/hansschuster/item-catalog).
[AWS Lightsail](https://aws.amazon.com/lightsail/) was used to deploy an
instance of [Ubuntu 16](https://www.ubuntu.com/).

## Basic information

- URL: [http://ec2-18-196-228-77.eu-central-1.compute.amazonaws.com/restaurants/](http://ec2-18-196-228-77.eu-central-1.compute.amazonaws.com/restaurants/)
- IP address: 18.196.228.77
- SSH port: 2200

## Installed packages

- apache2 (apt-get)
- libapache2-mod-wsgi (apt-get)
- postgresql (apt-get)
- python-flask-sqlalchemy (apt-get)
- python-psycopg2 (apt-get)
- python-httplib2 (apt-get)
- python-requests (apt-get)
- python-oauth2client (apt-get)
- Checked that python2, Flask and git are installed and at newest version
- Ran `apt-get update` and `upgrade` at beginning and end of project

## Configurations

- Added port 2200 to Lightsail instance firewall
- Changed ssh port to 2200 in `etc/ssh/sshd_config`
- Configured *ufw* to only allow connections for ports 2200 (SSH), 80 (HTTP)
  and 123 (NTP)


- Created new user *grader*
- Added file *grader* in directory `/etc/sudoers.d/` and gave sudo rights
- Created key-pair and saved public key in `/home/grader/.ssh/authorized_keys`


- Set timezone to UTC with `sudo dpkg-reconfigure tzdata`
- Checked that `PasswordAuthentication` is set to no in `/etc/ssh/sshd_config`
- Changed to `PermitRootLogin no` in `/etc/ssh/sshd_config` to disallow remote
  login for user *root*; Afterwards `sudo service ssh restart`


- Added `WSGIScriptAlias / /var/www/html/myapp.wsgi` to
  `/etc/apache2/sites-enabled/000-default.conf`
- Added file `/var/www/html/myapp.wsgi` with content
  `from yourapplication import app as application`


- Created Postgresql db user *catalog* with limited permissions:
  `sudo -u postgres createuser --interactive`
- Created Postgresql database *catalog*
- Added rights to user *catalog* to access db tables; Also added rights to use
  sequence to increase *ID*
- Checked that remote connections are not allowed in
  `/etc/postgresql/9.5/main/pg_hba.conf`


- In Google Console added:
  - Authorized JS Origins:
    'http://ec2-18-196-228-77.eu-central-1.compute.amazonaws.com'
  - Authorized redirect URIs:
    'http://ec2-18-196-228-77.eu-central-1.compute.amazonaws.com/login' and
    'http://ec2-18-196-228-77.eu-central-1.compute.amazonaws.com/gconnect'
- Exchanged content accordingly in `/var/www/html/client_secret.json`

## Third party resources

- AWS Lightsail with an instance of Ubuntu 16
- Google OAuth 2.0 for Login
