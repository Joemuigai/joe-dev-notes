<!-- Composer Installation Guide -->
# Composer Installation Guide

This guide will help you install Composer on a Linux system.

## Step 1: Download Composer

First, download the Composer installer using `curl`:

```sh
curl -sS https://getcomposer.org/installer | php
```

## Step 2: Move Composer Executable

Move the Composer executable to the `/usr/local/bin` directory to make it globally accessible:

```sh
sudo mv composer.phar /usr/local/bin/composer
```

You may need to make the Composer executable:

```sh
sudo chmod +x /usr/local/bin/composer
```

## Step 3: Verify Installation

Verify the Composer installation by checking the version:

```sh
composer --version
```

You should see the Composer version displayed in the output.
