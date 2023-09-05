### Curso de Magento 2

En este repositorio puede encontrar los ejemplos desarrollados durante el curso

Instalación de Magento

Apache

Instalar:
apt-get -y install apache2


Verificar:
apache2 -v

Habilitar rewrite
a2enmod rewrite
vim /etc/apache2/sites-available/000-default.conf
<Directory "/var/www/html">
    AllowOverride All
</Directory>

Evitar 403
<Directory "/var/www/">
  Options Indexes FollowSymLinks MultiViews
  AllowOverride All
  Order allow,deny
  Require all granted
</Directory>
systemctl restart apache2

MySQL (5.7 para no generar inconvenientes)
https://www.fosstechnix.com/how-to-install-mysql-5-7-on-ubuntu-22-04-lts/

PHP 8.2
apt-get install php
apt-get install php8.X-{bcmath,common,curl,fpm,gd,intl,mbstring,mysql,soap,xml,xsl,zip,cli}

Composer
apt-get install composer
Opensearch
https://opensearch.org/docs/latest/install-and-configure/install-opensearch/debian/
https://artifacts.opensearch.org/releases/bundle/opensearch/2.9.0/opensearch-2.9.0-linux-x64.deb
disable ssl
sudo vim /etc/opensearch/opensearch.yml
plugins.security.disabled: true
sudo systemctl restart opensearch

Instalar el metapackge

https://devdocs.magento.com/guides/v2.3/install-gde/composer.html

composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition <install-directory-name>
composer create-project --repository-url=https://8f7a95de6fbfbc275b53b8cf398d41dd:cbb31296ab51b2921df3d13981ca9ee2@repo.magento.com/ magento/project-community-edition magento

php bin/magento setup:install --base-url=http://localhost --db-host=localhost --db-name=magento --db-user=magento --db-password=magento --admin-firstname=admin --admin-lastname=admin --admin-email=admin@admin.com --admin-user=admin --admin-password=admin123 --language=en_US --currency=USD --timezone=America/Chicago --use-rewrites=1

php bin/magento sampledata:deploy
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy -f
Si hay problema desplegando contenido statico
php bin/magento config:set dev/static/sign 0
php bin/magento cache:clean
php bin/magento cache:flush
sudo chmod -R 777 *

php bin/magento setup:config:set --backend-frontname="admin"


Apache 2 rewrite
vim /etc/apache2/apache2.conf
<Directory /var/www/>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
</Directory>


php bin/magento admin:user:create --admin-user="jonathan" --admin-password="Jonathan2023*." --admin-email="jonathan@artd.com.co" --admin-firstname="Jonathan" --admin-lastname="Urzola"

deshabilitar el 2FA

bin/magento module:disable Magento_AdminAdobeImsTwoFactorAuth
bin/magento module:disable Magento_TwoFactorAuth
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy -f
Si hay problema desplegando contenido statico
php bin/magento config:set dev/static/sign 0
php bin/magento cache:clean
php bin/magento cache:flush
sudo chmod -R 777 *
