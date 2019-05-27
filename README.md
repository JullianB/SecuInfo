# **TP 1**

- installer apache \ créer le dossier administrator \ déplacer html/index.html dans administrator: 
    >*apt-get install apache2*
    *mkdir var/www/admnistrator*
    *mv var/www/html var/www/administrator*
    
- créer monsite.conf et y créer un VirtualHost \ Ajouter une authentification Basic:
    >*touch etc/apache2/sites-available/monsite.conf*
    >*vim monsite.conf*
    >*htpasswd -c [chemin] [user]*
    >
    ><VirtualHost *:80>
    >ServerName monsite.com
    >ServerAlias www.monsite.com
    >DocumentRoot var/www/administrator/html
    ><Directory "var/www/administrator/html/">
    >DirectoryIndex index.html
    >Options FollowSymLinks
    >AlowOverride All
    >Require user [user] 
    >AuthType basic
    >AuthName "private area"
    >AuthUserFile /etc/apache2/pass.txt [chemin password]
    ></Directory>
    ></VirtualHost>

- lancer monsite.conf

    >*a2dissite 000-default.conf*
    >*apache2ctl restart*
    >*a2ensite monsite.conf*
    >*apache2ctl restart*

- Accèder au site monsite.com 
    >*curl -u [user]:[passwd] [url]*

![capture](https://github.com/JabbM/SecuInfo/blob/master/CaptureWireSharkTP1_01.PNG)