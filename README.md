# Docker Compose files for online services selfhosting
My configuration files and instructions to duplicate my web apps settings. You should have already installed [Docker](https://docs.docker.com/get-docker/) and [Docker-compose](https://docs.docker.com/compose/install/) to run this apps.

After you have installed, download docker-compose.yml files to folder named by application (for example /home/user/docker/nextcloud/docker-compose.yml) and run command in terminal as sudo or root: 
``` 
# docker-compose up -d 
``` 
which run download and installation process of application. After it give you number of container (for example: 273442ec06ee) and your app should be running on adress in web browser: 
```
localhost:9090
``` 
Edit port number by your port number in configuration.

You must have port number exclusive for every application, or you will get error.

### For status of your container
```# docker ps```
You should see info like Up 1 minute.

### For hosting services under domain name
I'm using [Apache2 webserver](https://ubuntu.com/tutorials/install-and-configure-apache#2-installing-apache) for creating reverse proxy for my apps. So instead of adress example.com:9090 I can access my web-app with subdomain like drive.example.com 

Of course you need: 
- public IP adress from your internet provider like 89.190.46.52
- setup your PC or Router to fix your IP adress in LAN like 192.168.1.2
- setup your Router to port-forwarding of ports 80 and 443 (HTTP AND HTTPS)
- running apache2 with activated configuration file of your reverse proxy
- running docker container service (your app)

You will find example file to easy create Apache2 name server reverse proxy for your port, where you have your app running.
Config file should be inserted in
```
/etc/apache2/sites-available/drive.example.com.conf
```

and activated by:

```
# a2ensite drive.example.com.conf
# systemctl reload apache2
```

### HTTPS protocol for Apache2 websites
I'm using Let's encrypt certificates. For managing certificates I'm usig Certbot app. It's very easy to setup your web to use HTTPS with this app. Just follow instructions to [install certbot](https://certbot.eff.org/instructions). After installation just run as root:
```
# certbot --apache
```
and choose your name website to obtain HTTPS.

Backup your cert files! I recomment to save complete folder ```/etc/letsencrypt``` to be able to restore your previous certificates in case of system failiture.
