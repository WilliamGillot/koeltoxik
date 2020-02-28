# Documentation

## Présentation
```bash
[Lien de la présentation] (https://www.canva.com/design/DAD1GkHHv_Q/quOE6o_ii10qIKzrpJ7FTA/view?utm_content=DAD1GkHHv_Q&utm_campaign=designshare&utm_medium=link&utm_source=sharebutton&fbclid=IwAR1G7Pt1T8zxhEBWF1_YGUfD1B7f0-tGOz6sgU-_uOqTxCaPXd-dLiSOtv8)
```

## I- Pré-requis

**Matériels**
```bash
Raspberry Pi 4 (Raspbian Buster)
Livebox
```

## II- Installation et initialisation du projet

**Configuration de la raspberry**
```bash
Installation de raspbian 10 (Buster)
Ouverture et fowarding des ports 22, 80, 443 et 8000
Mise en place de clé privée pour désactiver la connection ssh par mot de passe
```

**Installation des dépendances**
```bash
php7.3
php7.3-mysql
PHP7.3-xml
php7.3-mbstring
php7.3-curl
php7.3-zip
MariaDB
```

**Clonage du dépot git et attribution de droit**
```bash
git clone --recurse-submodules https://github.com/phanan/koel.git
git checkout v4.2.2
chown -R www-data:www-data /var/www/koel
```

**Création d'une base de donnée**
```bash
sudo mysql -u root -p
mysql> CREATE DATABASE koel DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
mysql> CREATE USER 'koel-db-user'@'localhost' IDENTIFIED BY 'koel-pass';
mysql> GRANT ALL PRIVILEGES ON koel.* TO 'koel-db-user'@'localhost' WITH GRANT OPTION;
mysql> exit;
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

**Installation de composer et npm**
```bash
npm install (enlever cypress du package.json si il y a une erreur et ajouter les assets à la main)
npm install yarn -g
composer install
```

**Lancement du projet et du serveur à l'aide de php artisan**
```bash
php artisan koel:init
php artisan serv
```

**Vérification sur localhost**
```bash
Vérifier le premier rendu visuel sur http://localhost:8000
```

## III- Mise en place d'un reverse Proxy

**Création d'un vHost pour ajouter koel en sous domaine**
```bash
vim etc/nginx/sites-available/koel.conf

sudo ln -s /etc/nginx/sites-available/koel.conf /etc/nginx/sites-enabled/
```

**Configuration de Nginx**

[Générateur de fichier Nginx](https://www.digitalocean.com/community/tools/nginx)

[Exemple de configuration pour koel](https://github.com/phanan/koel/blob/master/nginx.conf.example)


**Lancement de Nginx**
```bash
sudo service nginx restart
sudo systemctl enable nginx
```

## IV- Mise en place d'une backup

**sous titre**
```bash

```

## V- Mettre à jour Koel

**Regarder la dernière version disponible**

[Lien du dépôt des Maj](https://github.com/phanan/koel/releases)


**Mettre à jour**
```bash
git checkout v4.2.2
```
