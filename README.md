# Godot + Laravel

- [Dependencies](DEPENDENCIES.md)

# Explanation
- [My Youtube channel](https://youtube.com.br/thiagobruno)

# Setting
- Clone this repository
- cd godot_laravel/laravel
- Execute:
    - composer install
    - chmod -R 0777 storage
    - chmod -R 0777 bootstrap/cache
    - cp .env.model .env
    - php artisan key:generate
    - create mysql database ```godot_laravel```
    - config the ```.env``` file with your parameters
    - php artisan migrate
    - php artisan passport:install

    ## Optimize
    - php artisan optimize:clear

    ## local serve
        - php artisan serve
        - Access: [http://127.0.0.1:8000](http://127.0.0.1:8000)

# Config local Apache
- ```sudo nano /etc/hosts```
    ```bash
    # add this line
    127.0.0.1   godotlaravel.local
    ```
- ```cd /etc/apache2/sites-available```
- ```sudo nano api-godotlaravel.conf```
    ```bash
    <VirtualHost *:80>
        ServerName godotlaravel.local
        ServerAlias godotlaravel.local

        ServerAdmin webmaster@localhost
        DocumentRoot "/home/SEU_USUARIO/Godot_Laravel/laravel/public"

        <Directory "/home/SEU_USUARIO/Godot_Laravel/laravel/public">
                AllowOverride all
                Require all granted
        </Directory>
    </VirtualHost>
    ```
- ```sudo a2ensite api-godotlaravel.conf```
- ```sudo systemctl restart apache2```
- Test: [http://godotlaravel.local](http://godotlaravel.local)

# Deploy production server
- Edit ```.env``` file
    ```bash
    APP_ENV=production
    APP_DEBUG=false
    ```
- composer install --optimize-autoload --no-dev

## Config cache
- php artisan config:cache
- php artisan route:cache