# **TP 1**

- installer apache \ créer le dossier administrator \ déplacer html/index.html dans administrator: 

        apt-get install apache2
        mkdir var/www/admnistratorBasic
        mv var/www/html var/www/administratorBasic
    
- créer monsite.conf et y créer un VirtualHost \ Ajouter une authentification Basic:

        touch etc/apache2/sites-available/monsite.conf
        vim monsite.conf
        htpasswd -c [chemin] [user]
        
        <VirtualHost *:80>
        ServerName monsite.com
        ServerAlias www.monsite.com
        DocumentRoot var/www/administratorBasic/html
        <Directory "var/www/administratorBasic/html/">
        DirectoryIndex index.html
        Options FollowSymLinks
        AllowOverride All
        Require valid-user 
        AuthType basic
        AuthName "private area Basic"
        AuthUserFile [chemin du fichier contenant le password]
        </Directory>
        </VirtualHost>

- lancer monsite.conf

        a2dissite 000-default.conf
        apache2ctl restart
        a2ensite monsite.conf
        apache2ctl restart

- Accèder au site monsite.com 

        curl -u [user]:[passwd] [url]

![capture](https://github.com/JabbM/SecuInfo/blob/master/CaptureWireSharkTP1_01.PNG)

- Utiliser OpenSSL pour décoder le challenge:

        echo "c2F0YW46cGFzc3dk" | openssl enc -base64 -d
        
- Créer un nouveau site avec une authentification Digest \ et creer le fichier contenant le user et mot de passe:

        htdigest -c pass2.txt "private area Digest" satan

        <VirtualHost *:80>
        ServerName monsite2.com
        ServerAlias www.monsite2.com
        DocumentRoot var/www/administratorDigest/html
        <Directory "var/www/administratorDigest/html/">
        DirectoryIndex index.html
        Options FollowSymLinks
        AllowOverride All
        Require valid-user 
        AuthType digest
        AuthName "private area Digest"
        AuthUserFile [chemin du fichier contenant le password]
        </Directory>
        </VirtualHost>
        
![capture](https://github.com/JabbM/SecuInfo/blob/master/CaptureWireSharkTP1_02.PNG)
