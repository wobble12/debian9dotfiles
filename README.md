# debian9dotfiles


## Installation de PHP 7.2

On ajoute une clé GPG pour les paquets PHP, depuis le serveur de celui qui fait les paquets debian et ubuntu officiels.
```bash
# wget -q https://packages.sury.org/php/apt.gpg -O- | sudo apt-key add -
```
*Normalement, vous reçevez comme message "OK"*

Ensuite, on ajoute ce dépôt dans notre liste de dépôts
```bash
# echo "deb https://packages.sury.org/php/ stretch main" | sudo tee /etc/apt/sources.list.d/php.list
```
*Normalement vous reçevez comme message "deb https://packages.sury.org/php/ stretch main"*

On met à jour notre liste de dépôts, puis on installe PHP 7.2
```bash
# sudo apt-get update
```
*Lisez bien, vous reçevrez peut être un message comme quoi il vous manque un paquet, installez le et relancez l'opération*
```bash
# sudo apt-get install php7.2 php7.2-xml php7.2-zip php7.2-mysql
```

## Installation de MariaDB (Serveur de base de données)
```bash
# apt-get install mariadb-server
# mysql_secure_installation
```

## Installation de node.js et npm
On installe curl, un outil qui nous permettra d'installer le nouveau dépôt
```bash
# apt-get install curl
```
On ajout le dépôt de node : 
```bash
$ curl -sL https://deb.nodesource.com/setup_8.x | sudo bash -
```
On installe nodejs (qui contient automatiquement npm)
```bash
# apt-get install -y nodejs
```

## Installation de composer 
```bash
# apt-get install composer
```

## Configuration du projet
Afin d'être sûr que les configurations ci dessus aient été prises en compte, on redémarre le serveur apache :
````bash
# systemctl restart apache2
````

Ajout de l'utilisateur au groupe www-data : 
```bash
# adduser username www-data
```
Gestion des permissions par défaut : 
```bash
# chown -R www-data:www-data /var/www/
# find /var/www/ -type d -exec chmod 775 "{}" \;
# find /var/www/ -type f -exec chmod 664 "{}" \;
# find /var/www -type d -exec chmod g+s "{}" \;
```
Gestion des permissions du dossier var avec l'outil ACL : 
```bash
# apt-get install acl
# cd /dossier/du/projet/symfony
$ sudo setfacl -dR -m u:www-data:rwX -m u:$(whoami):rwX var
$ sudo setfacl -R -m u:www-data:rwX -m u:$(whoami):rwX var
```
