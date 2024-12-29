<!-- Postgresql fresh installation on linux -->

# Postgresql fresh installation on linux

Postgresql is a powerful, open source object-relational database system. It has more than 15 years of active development and a proven architecture that has earned it a strong reputation for reliability, data integrity, and correctness. It runs on all major operating systems, including Linux, UNIX (AIX, BSD, HP-UX, SGI IRIX, Mac OS X, Solaris, Tru64), and Windows.

In this article, we will install Postgresql on a Linux machine.

## Prerequisites

- A Linux machine
- A user account with sudo privileges
- The apt package manager, included by default in Ubuntu

## Uninstalling Postgresql

Before uninstalling any software, especially a database system, ensure you have backed up all your essential data. Use the pg_dump tool or any other preferred method to backup your PostgreSQL databases.

If you have an existing installation of Postgresql on your system, you can uninstall it using the following commands:

```bash
sudo systemctl stop postgresql
sudo apt-get --purge remove postgresql\*
sudo deluser postgres
sudo delgroup postgres
sudo rm -rf /etc/postgresql/
sudo rm -rf /var/lib/postgresql/
sudo rm -rf /var/log/postgresql/
sudo apt autoremove
sudo apt autoclean
sudo apt-get update
```

This will remove Postgresql and its associated packages from your system.


## Step 1: Update the system

Before installing any software, it's always a good idea to update the system to the latest packages. This ensures that you are installing the latest versions available.

```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install Postgresql

Postgresql is available in the default Ubuntu repositories, so you can install it using the apt package manager.

```bash
sudo apt install postgresql postgresql-contrib
```

This command will install Postgresql and some additional utilities that are useful for administering a Postgresql server.

## Step 3: Verify the installation

Once the installation is complete, you can verify it by checking the version of Postgresql that was installed.

```bash
psql --version
```

This command will output the version of Postgresql that is installed on your system.

```bash
sudo -u postgres psql -c "SHOW config_file"

sudo nano /etc/postgresql/14/main/postgresql.conf

# listen_addresses = 'localhost'         # what IP address(es) to listen on;
```

This command will output the location of the Postgresql configuration file.


## Step 4: Access the Postgresql prompt

You can access the Postgresql prompt by running the following command:

```bash
sudo -u postgres psql
\password postgres
```

This command will log you in as the Postgresql user and open the Postgresql prompt. From here, you can interact with the Postgresql server using SQL commands.

## Step 5: Configure Postgresql

By default, Postgresql is configured to use the peer authentication method for local connections. This means that the Postgresql user can log in without a password if they are logged in as the Postgresql user on the system.

If you want to change the authentication method to require a password for local connections, you can do so by editing the `pg_hba.conf` file.

```bash
sudo nano /etc/postgresql/<version>/main/pg_hba.conf
```

Find the following lines in the file:

```bash
local   all   postgres   peer
```

Change `peer` to `md5`:

```bash
local   all   postgres   md5
```

Save the file and restart the Postgresql service:

```bash
sudo systemctl restart postgresql
```

This command will log you in as the Postgresql user and open the Postgresql prompt. From here, you can interact with the Postgresql server using SQL commands.

## Conclusion

You have successfully installed Postgresql on your Linux machine. You can now start using Postgresql to store and manage your data.

For more information on how to use Postgresql, you can refer to the official documentation: [Postgresql Documentation](https://www.postgresql.org/docs/)
