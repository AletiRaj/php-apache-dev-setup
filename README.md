# PHP Apache Development Setup (Windows 11)

A native Windows 11 development environment using Apache 2.4, PHP 8.4, MySQL 8.4, Composer, Node.js, VS Code and Xdebug without Docker.

## Environment Overview

| Component | Version                   |
| --------- | ------------------------- |
| Apache    | 2.4                       |
| PHP       | 8.4.22                    |
| MySQL     | 8.4                       |
| Composer  | 2.10.1                    |
| Node.js   | 24.x                      |
| npm       | 11.x                      |
| VS Code   | Latest                    |
| Xdebug    | Latest compatible version |

---

## Folder Structure

```txt
F:\devtools
│
├── apache24
│
├── php84
│
└── htdocs
    ├── index.html
    └── info.php

F:\databases
│
└── mysql
```

---

## Download Links

### Apache 2.4

https://www.apachelounge.com/download/

### PHP 8.4

https://windows.php.net/download/

### MySQL 8.4

https://dev.mysql.com/downloads/mysql/

### Composer

https://getcomposer.org/download/

### Node.js

https://nodejs.org/en/download

### Visual Studio Code

https://code.visualstudio.com/download

### Xdebug

https://xdebug.org/wizard

---

## Apache Configuration

### Enable Rewrite Module

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

### PHP Integration

```apache
LoadModule php_module "F:/devtools/php84/php8apache2_4.dll"

PHPIniDir "F:/devtools/php84"

AddHandler application/x-httpd-php .php

DirectoryIndex index.php index.html
```

### ServerName

```apache
ServerName localhost:80
```

---

## PHP Configuration

### php.ini

```ini
extension_dir = "F:\devtools\php84\ext"

extension=curl
extension=fileinfo
extension=gd
extension=intl
extension=mbstring
extension=mysqli
extension=openssl
extension=pdo_mysql
extension=sodium
extension=zip

memory_limit=512M
upload_max_filesize=64M
post_max_size=64M
max_execution_time=120
date.timezone=Asia/Kolkata
```

---

## MySQL Configuration

### Data Directory

```txt
F:\databases\mysql
```

### Verify

```sql
SHOW VARIABLES LIKE 'datadir';
```

---

## Virtual Host Example

### httpd-vhosts.conf

```apache
<VirtualHost *:80>
    ServerName medisyslocal.com

    DocumentRoot "F:/devtools/apache24/htdocs/medisys/public"

    <Directory "F:/devtools/apache24/htdocs/medisys/public">
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

### Hosts File

```txt
127.0.0.1 medisyslocal.com
```

File Location:

```txt
C:\Windows\System32\drivers\etc\hosts
```

---

## Xdebug Configuration

### php.ini

```ini
zend_extension=xdebug

xdebug.mode=debug,develop
xdebug.start_with_request=yes
xdebug.client_host=127.0.0.1
xdebug.client_port=9003
```

### VS Code launch.json

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "port": 9003
        }
    ]
}
```

---

## Verification Commands

### Apache

```cmd
httpd -t
httpd -v
```

### PHP

```cmd
php -v
php -m
```

### Composer

```cmd
composer -V
composer diagnose
```

### MySQL

```cmd
mysql -u root -p
```

### Node.js

```cmd
node -v
npm -v
```

---

## Common Issues & Fixes

### PHP Extensions Not Loading

Problem:

```txt
Unable to load dynamic library
```

Fix:

```ini
extension_dir = "F:\devtools\php84\ext"
```

---

### Apache ServerRoot Error

Problem:

```txt
ServerRoot must be a valid directory
```

Fix:

```apache
Define SRVROOT "F:/devtools/apache24"
ServerRoot "${SRVROOT}"
```

---

### Composer Using Wrong PHP Version

Problem:

```txt
Composer using PHP 8.3
```

Fix:

Update composer.bat:

```bat
@echo off
"F:\devtools\php84\php.exe" "C:\Users\<user>\bin\composer.phar" %*
```

---

### Invalid URI: Scheme is malformed

Problem:

```txt
Invalid URI: Scheme is malformed
```

Fix:

```env
APP_URL=http://your-domain.local
```

---

### Laravel Cannot Connect to MySQL

Problem:

```txt
php_network_getaddresses
```

Fix:

```env
DB_HOST=127.0.0.1
```

Do not use:

```env
DB_HOST=mysql
```

for native Windows installations.

---

## Repository Purpose

This repository stores:

* Apache configuration
* PHP configuration
* Virtual Host configuration
* Xdebug configuration
* Development environment setup

It does not contain application source code.

---

## License

For educational and development environment setup purposes.
