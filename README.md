# Liliana's Trade

This is the repo of the Liliana's Trade website!

It's a Django project that manage collection of magic card.

> Website available at address: [lilianastrade.h.minet.net](http://lilianastrade.h.minet.net)

## Table of Contents

- [App Structure](#app-structure)
- [Users](#users)
- [Installation](#installation)
- [Deploy](#deploy)
- [Authors](#authors)

## App Structure

- [Controller/](src/Controller): The controllers of the website
- [DataFixtures/](src/DataFixtures): The data fixtures of the website
- [Entity/](src/Entity): the entities of the website
- [Form/](src/Form): the forms of the website
- [Repository/](src/Repository): the repositories of the website

## Users

3 users :

* User
  * user@email.com
  * 1234

* Skyfred
  * skyfred@gmail.com
  * skyfredthebest

* Wolffair
  * juliette.debono2002@gmail.com
  * password

## Installation

1. Clone git repository

    ```bash
    git clone git@github.com:juliette39/lilianastrade.git
    ```
   
2. Install PHP 8.1 (Linux)

    ```bash
    sudo apt-get update
    sudo apt-get install ca-certificates apt-transport-https software-properties-common wget curl lsb-release
    curl -sSL https://packages.sury.org/php/README.txt | sudo bash -x
    sudo apt-get update
    sudo apt-get install php8.1
    sudo apt-get install libapache2-mod-php8.1
    sudo systemctl restart apache2
    php -v
    ```

3. Install the dependencies (Linux)

    ```bash
    sudo apt update
    sudo apt full-upgrade
    
    sudo apt install php8.1-cli
    sudo apt install php8.1-xml php8.1-sqlite3 php8.1-intl php8.1-mbstring
    php -m | grep "xml\|sqlite\|intl"
        intl
        libxml
        pdo_sqlite
        sqlite3
        xml
        xmlreader
        xmlwriter
    curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
    sudo apt-get install php-zip
    sudo apt install symfony-cli
    sudo apt install sqlite3
    symfony check:requirements
    symfony composer -V
   ```

4. Reload composer and the database

    ```bash
    rm -fr composer.lock symfony.lock var/cache/ vendor/
    symfony composer update
    symfony composer install
   
    symfony console doctrine:database:drop --force
    symfony console doctrine:database:create
    symfony console doctrine:schema:create
    symfony console doctrine:fixtures:load -n
    ```

5. Launch the website
    ```bash
    symfony server:start
    ```

## Deploy

You need to configure your VM.

After installing the project as explained in [Installation](#installation)

Put the repo in `/var/www/lilianastrade`

Then run the authorizations:

```bash
sudo chmod 777 /var/www/lilianastrade/var/log/dev.log
sudo chown www-data:www-data /var/www/lilianastrade/var/log/dev.log
```

Then configure the VM as follows:

```bash
sudo nano /etc/apache2/sites-available/myconfig.conf
```

```
<VirtualHost *:80>
    ServerName lilianastrade.h.minet.net
    DocumentRoot /var/www/lilianastrade/public

    <Directory /var/www/lilianastrade/public>
        AllowOverride None
        Require all granted
        Allow from All

        FallbackResource /index.php
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

You load the configuration and restart the apache server
```bash
sudo a2ensite myconfig.conf
sudo service apache2 restart
```

> To unload a configuration: `sudo a2dissite myconfig.conf`

## Authors

- Juliette Debono
