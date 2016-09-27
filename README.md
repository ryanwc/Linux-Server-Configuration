# Linux Server Configuration

This is not a traditional project; it is a snapshot of relevant information about a linux server I have set up to host another project -- [Restaurant Manager](https://github.com/ryanwc/RestaurantManager).

The server is built using Linux (Ubuntu distro), Apache, and Amazon Web Services technology.

The application it serves (Restaurant Manager, linked above) is built using python, flask, postgresql, sqlalchemy, and the usual front-end languages.

Apparently, the AWS instance will be deleted sometime soon.  Sorry if that has already happened.

# Project Details

## IP Address and SSH Port

The IP address for the server is: 52.38.172.72  
The port on which the server accepts SSH is: 2200

## URL to the Hosted Web Application

The complete URL to the hosted Restaurant Manager application is:  
http://ec2-52-38-172-72.us-west-2.compute.amazonaws.com/

## Summary of Software Installed and Configuration Changes

Here is an exerpt of the .bash_history showing relevant changes:

```
6  sudo adduser grader  
10  cd sudoers.d  
12  sudo nano README  
15  sudo nano sudoers  
```  
create a user called grader and give it sudo

```
24  sudo apt-get update  
25  sudo apt-get upgrade  
```  
update / upgrade software

```
26  sudo dpkg-reconfigure tzdata  
```  
set the local time to UTC

```
28  sudo nano /etc/ssh/sshd_config  
```  
configure ssh

```
29  sudo ufw allow 2200  
30  sudo ufw allow 80  
31  sudo ufw allow 123  
32  sudo ufw enable  
33  sudo ufw status  
```  
configure and enable firewall

``` 
36  sudo apt-get install apache2  
```  
install apache

```
40  apt-get install postgresql-9.3  
42  sudo psql  
43  create role root  
```  
install postgresql and create a role (remote access disabled by default)  

```
50  sudo apt-get install git-all  
56  git clone https://github.com/ryanwc/RestaurantManager  
```  
install git and clone the app to host

```
59  sudo apt-get install libapache2-mod-wsgi python-dev  
60  sudo a2enmod wsgi  
61  sudo apt-get install python-pip  
62  sudo pip install virtualenv  
63  sudo virtualenv restman  
64  source restman/bin/activate  
65  sudo pip install Flask  
```  
install and set config to let ubuntu/apache serve a flask app

```
72  cp -R RestaurantManager/restman /var/www  
76  rm -r restman  
78  sudo nano instance/config.py  
79  sudo nano run.py  
80  sudo nano restaurantmanager/__init__.py  
81  pip install SQLAlchemy  
82  pip install bleach  
83  pip install --upgrade oauth2client  
89  sudo nano /etc/apache2/sites-available/RestaurantManager.conf  
90  sudo a2ensite RestaurantManager  
92  sudo nano restaurantmanager.wsgi  
95  sudo a2enconf RestaurantManager  
116  sudo a2ensite RestaurantManager.conf  
117  sudo a2enconf RestaurantManager.conf  
119  sudo a2dissite 000-default.conf  
```  
various changes to get app working

```
171  sudo apt-get install python-psycopg2  
173  sudo nano /etc/hostname  
174  sudo nano /etc/hosts  
189  sudo nano pg_hba.conf  
191  psql -d catalog -U catalog  
192  sudo nano pg_hba.conf  
205  sudo nano host.conf  
206  sudo nano hosts.allow  
207  sudo nano hosts.deny  
229  createdb catalog  
247  sudo nano restaurantmanager/database_setup.py  
288  sudo nano InitPopScript.py  
291  sudo nano DataManager.py  
334  sudo nano index.html  
344  sudo nano g_client_secrets.json  
391  sudo pip install werkzeug==0.8.3  
392  sudo pip install flask==0.9  
393  sudo pip install Flask-Login==0.1.3  
```  
various changes to get postgresql working with the app (including downgrading some software)
note the app was originally writted for sqlite, migrating was painless

```
  408  chmod 777 pics  
```  
enable writing and reading from to pics folder so the server can store and serve uploaded pics
probably not the best security policy but it works for this project

```
481  sudo nano /etc/ssh/sshd_config  
483  sudo visudo  
485  su grader  
491  sudo nano passwd  
492  passwd grader  
493  passwd  
509  sudo adduser grader sudo  
```  
ensure grader has sudo and ssh is properly working

```
516  sudo nano /etc/ssh/sshd_config  
```  
disable remote login for root

## List of Third-Party Resources

This project makes use of the following resources:

- Linux (Ubuntu distro)
- Amazon Web Services (AWS)
- apache2
	- sudo apt-get install apache2
- mod_wsgi
	- sudo apt-get install libapache2-mod-wsgi python-dev
- git
	- sudo apt-get install git-all
- pip
	- sudo apt-get install python-pip 
- virtualenv
	- sudo pip install virtualenv 
- sqlalchemy
	- pip install SQLAlchemy
- bleach
	- pip install bleach
- oauth2client
	- pip install --upgrade oauth2client
- flask
	- sudo pip install Flask
- postgresql
	- apt-get install postgresql-9.3
- psycopg2
	- sudo apt-get install python-psycopg2

# Feedback

Any feedback about your experience using the app is welcome.  Please send feedback to [ryanwc13@gmail.com](mailto:ryanwc13@gmail.com).

# License

No specifics yet.