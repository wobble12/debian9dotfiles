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
# sudo apt-get install php7.2
```