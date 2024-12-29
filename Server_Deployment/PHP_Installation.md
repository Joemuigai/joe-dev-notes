# PHP Installation Guide

This guide will help you install PHP 8.4 and the necessary extensions on a Linux system.

## Uninstall Previous PHP Versions

If you have an older version of PHP installed on your system, you should uninstall it before proceeding with the installation of PHP 8.4.

```sh
sudo apt-get purge php*.*
```

After uninstalling the previous PHP version, you can clean up the system by running the following commands:

```sh
sudo apt-get autoremove
sudo apt-get autoclean
```

## Install PHP 8.4

## Step 1: Add PHP Repository

First, add the repository that contains the PHP packages:

```sh
sudo add-apt-repository ppa:ondrej/apache2
```

## Step 2: Update Package List

Update the package list to include the newly added repository:

```sh
sudo apt-get update
```

## Step 3: Install PHP 8.4

Install PHP 8.4 using the following command:

```sh
sudo apt-get install php8.4
```

## Step 4: Install Required Extensions

Install the necessary PHP extensions for your project. Here are some common extensions:

```sh
sudo apt-get install libapache2-mod-php8.4 php8.4-bcmath php8.4-mbstring php8.4-mysql php8.4-xml php8.4-zip php8.4-curl php8.4-gd php8.4-redis php8.4-intl php8.4-soap
```

## Step 5: Verify Installation

Verify the PHP installation by checking the version:

<!-- echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php -->

Create a PHP file with the following content:

```sh
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/info.php
```

Open a web browser and navigate to `http://your_server_ip/info.php`. You should see the PHP information page.

Alternatively, you can check the PHP version from the command line:

```sh
php -v
```


You should see the PHP version displayed in the output.

## Step 6: Configure PHP

You can configure PHP settings by editing the `php.ini` file. The location of the `php.ini` file may vary depending on your system configuration.

## Step 7: Restart Web Server

If you are using PHP with a web server like Apache, restart the web server to apply the changes:

```sh
sudo systemctl restart apache2
```

Congratulations! You have successfully installed PHP 8.4 on your Linux system.

Make sure to remove the info.php file after testing, as it can expose sensitive information about your PHP configuration:

```sh
sudo rm /var/www/html/info.php
```
