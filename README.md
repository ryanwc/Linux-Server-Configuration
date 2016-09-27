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

`
    6  sudo adduser grader
   10  cd sudoers.d
   12  sudo nano README
   15  sudo nano sudoers
`
create a user called grader and give it sudo

`
   24  sudo apt-get update
   25  sudo apt-get upgrade
`
update / upgrade software

`
   26  sudo dpkg-reconfigure tzdata
`
set the local time to UTC

`
   28  sudo nano /etc/ssh/sshd_config
`
configure ssh

`
   29  sudo ufw allow 2200
   30  sudo ufw allow 80
   31  sudo ufw allow 123
   32  sudo ufw enable
   33  sudo ufw status
`
configure and enable firewall

` 
   36  sudo apt-get install apache2
`
install apache

`
   40  apt-get install postgresql-9.3
   42  sudo psql
   43  create role root
`
install postgresql and create a role

`
   50  sudo apt-get install git-all
   56  git clone https://github.com/ryanwc/RestaurantManager
`
install git and clone the app to host

`
   59  sudo apt-get install libapache2-mod-wsgi python-dev
   60  sudo a2enmod wsgi
   61  sudo apt-get install python-pip
   62  sudo pip install virtualenv
   63  sudo virtualenv restman
   64  source restman/bin/activate
   65  sudo pip install Flask
`
install and set config to let ubuntu/apache serve a flask app

`
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
`
various changes to get app working

`
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
`
various changes to get postgresql working with the app (including downgrading some software)
note the app was originally writted for sqlite, migrating was painless

`
  408  chmod 777 pics
`
enable writing and reading from to pics folder so the server can store and serve uploaded pics
probably not the best security policy but it works for this project

`
  481  sudo nano /etc/ssh/sshd_config
  483  sudo visudo
  485  su grader
  491  sudo nano passwd
  492  passwd grader
  493  passwd
  509  sudo adduser grader sudo
`
ensure grader has sudo and ssh is properly working

`
  516  sudo nano /etc/ssh/sshd_config
`
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

## Udacity (user 'root') SSH Private Key

-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAsUbvnwd6a0NK0E4empLIUtzpqwzDdEeqLJCJZUn+5JsXJ3CM
qNT4EU2U0Zw7441n1OSspNgYaLE9/jp97bB38HrdpdH8fDpzE7yV5B0eRB/DCH3g
8MU3QanUxIWZy41KVKl1KCPEWk5UuwTsbe0MlEMWCy4uZ/2NlbPb2s1OfNBzpKAK
XfGKhIahpeQ9qMDIl/FF+JMrhk38HdcGL5grnOpB0B72FZM+F3A3BD+YdKaiJxka
2BV26hyNaBwROL3asI3dRB2Q4wvZUbAJnbgvCXIrO5iNwOazxVlqZKZSrBqpH3iF
EHNynXVqO8bvnhRmHzHrD7JNHQ8DxqTV+n5JIwIDAQABAoIBAC4nD59RbRebz1Bn
5iPL7wdTqCn2CrStK6qqfnq2RvvxPJfx/0y9FVA76HChwh295LhSSHgqIkCvVDpp
s/s7pB4hfq76+kbFWMxcnpFi20xVEIuXagaE8ZvQwSngtmd+A0oDTBMFLMtt9TUz
VPJRcqLuzEBg54f/ROsihixyoupvUzJ12nefRSfDJhcsBpjaU8zaf5PEUgTDDfg9
J1/VDQTrR5tBsmYR8zyzdo28OxAOpxmFmbzEQpz/CYMZ5xplwpG63I2HVAeM9OfC
EhweQU4Sq5u1VBpRMsOz0fvzbZIwgVe+3po4Nz2sgRl0eAU23eCnYvRV5/u7XRj5
AuUR2SECgYEA6Ineu11ng18Ty6xtD0heq66mKz2F0JshrBitahj5LJR0pNZ7TDxp
NtX/8pYDi+yIxT5i5nFP4tdn3GL4j9cWyuix0bOfNwpWQ3m4UTHMKhOvY0NdSkG7
S//0Z71qz6xpuAx11uQ6qKlcwCnMFFbzLBLutHCpYojSvLSek4dmQnsCgYEAwym+
Uuk6C1you5eqxMtg7s0NGdtApHPYKJmYpViaTVrbg16/VhGiZtJtfNupqC4Q+NgT
oaA1INKdEUEalwNLONbupWFxRiXgKP4+VOlZzEyx69qRwAk/b0J1wngZMIMQ4ovp
DFJ4UwhbD5auw3xw6YNYnXapL3QL5FafH5Quh3kCgYEA4WnscEIN+soqnVAK9Dqa
EuCdEeN0mRAYZwQQ7n1A5dcO708+fFs/PrnZfyWuUHA88L8WDf6fiux2MKv7+Stu
W8mPvhDZ8PfjQUt3wbV9DPjCFn4Rq87mKbj3Ca0TIjcm0BO8E1BwEFkEoP6jZsAW
v42muWFQwUSSy/xmj+o71YsCgYByhLQhgqmEsUJxkXWrNIwUlE3ztiwgU7mrWTWx
EGS6r23PkHFF1+Mr4p5Mfbj37tAWtPQQCyohsHRqA4HOyygAml4+vQby2pbGdyms
OaFvuDFO7FpKDSMj7iObkU12ofHufZqqmFnynxyP8SNrokG/REtjWpW8OqQfwJRu
u0zyQQKBgB1P7Ce7Gmn1wvlTwXq9vQ7diAE8n8mAC0O9mP/xoYDlhuVxsDXCrooh
EnMlFS6msppjbkMGllHDh6VDNMLXhGhlelM9S//C/w0w+SyMiegM9qFWVg61ETBB
MgGH8w5xQD35d+nooU2D2Mxb6JMbGWT/WHyse3cTwnnzqWh4ZIA7
-----END RSA PRIVATE KEY-----

## User 'grader' SSH Private Key

-----BEGIN RSA PRIVATE KEY-----
Proc-Type: 4,ENCRYPTED
DEK-Info: AES-128-CBC,277385BC47A0780D34F9C7C82614DEE5

YUd/MojSxw6hgMcIS00fDyfxZkV2zlPcx1c+rq4lHNb2Gv/4gnH5qsWQqYCUpuz1
3dmPoeTXWsZq1z2/vvZ2gbRpMnrDeK21gx1IvnXbB0sitXk9dlXGhgUPJqeZ7rUA
8Z+M6qLha+IBeH/IgUvqsN0IUFdTLrdiaO8lXdGX+SOGPFgeuHC7DootlOdF3LmD
WB1JF5QwVLwULlgvn5OeGcwGRl1EqiqCWo0VAzoyzGUCVOqs6bSxoNzNxnUZrMY2
9hYeVciUabgXwHOGBOFHqTz9uQaE4RpnV8c/XfPK8zdK7SrdH+6TRWkN13DQFxkB
JPeiK2Imex8KHrDqOwRDM175nte9ifYqCWwCR/EMoIy0coa7QF10os8CZaOTTs8K
3yv0OoGTn9EFeJw99Gf9lxsuBn/9WY4TV/wrXinuPArVJCGiJ7WiB/nehYKW4XKk
Z+g4z7ZIXxAsx9jtu9zJNWD/YVJDqeNv7aNVEDQAux97r/i7oal2w4kuck5M2xc8
j+0UkvuJBmwV5vXB3cNFg/8OqYCXm25zPUut/Y7SNfHO/TRpOrirY6C0gMb1AL+b
uXY77sE++sfhqov1ShaMH+UJ4tH/QKTThnOkeFrjRgLS1GcLMejs4BQp4jCyFBYu
nQYajMYgxSMeGN4hUayD19LQNwBd3USmqi7HSbtCTwWsIeCS4f4lgFqMTKIqYJH2
EKvbOeO+aIICcE03rDDDmWo2ZZKu7Z66gWgalr9xGokCl8ZpGbOyfXjVCFTtEW9v
dYYUN+yCmiltvaYheSDZPUPwol66yKkH6M0wlTmpPRBE2IUAtfnYnDi/TqIeLEJY
rGRL9U7Dz8Hh5DTo7rcKf6t0hEpyspq4ynI22mfdUVOGMczOUEwFyxg/duipOWQ5
59jGdU3YDQDCo3cwDTnuO/EMowzF95Y16H4ZTTtdYmdQ0ncWid65pvogplBGfTrP
uBI45w0R+f070benTvvhQmQqYxnKLl8jgELRhkNCW8ez2nWm2Aw9eWzhJFvrtEZ4
NlOPEeRdwNbSpOyCPxLGDG21PKpxcknOy0sOjRwGy4DVRvFLMhZHnGPdpF5LW4rx
v9e2vU1mFFCaUwoehsGVmwn9C0ZT/pMbtl6K0QKTKoHz5gn/z+dohDE0bw5VlKH9
VIZbWNpA2JNCvxDg2zkXVRxe5AsYi8exCFggsU5fx4+JpRJfLXlgYVlnKJeYoFXt
6EsaYEY5Kj2074ry57rLyjWAoB1CDknSyYt5egDiptKTty/HscRCBoGmv9OeoBK0
7yKkt32nu7k7b54VrZVJD6AdDeq0SxDfb/s2C7yvVh+/nNuX/pDD6VPMZS4O2nZf
AE+rtDvdWBBLv20x2I959l65OtZXN5wrll81/eia+DWtOfhjVJPq2dPCT+9ZnQZZ
RIhd2jiM6y05yk9EMBG4E+wy/dhnvFFlSHegz1qH+HYrd41NYdXWdtBq+D+pjix6
2zRA3K2dUZ/OHIRRX06rt5lX1wNBa5fh8TFzsTUaDOoUXml2KXGeH8jJDQjjQ3c8
TIy5PkchI1KMKU46RNugVzLuJgM88P86ta6caNJjzBopoKf5iXu9BVRMT7HORW03
-----END RSA PRIVATE KEY-----

# Feedback

Any feedback about your experience using the app is welcome.  Please send feedback to [ryanwc13@gmail.com](mailto:ryanwc13@gmail.com).

# License

No specifics yet.