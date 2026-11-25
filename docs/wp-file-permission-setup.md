# Secure WordPress File and Folder Permissions (Ubuntu + Apache/Nginx)

Replace `/var/www/html/your-site` with your site's path. The web server user is `www-data` on Ubuntu.

## 1. Set ownership

```bash
sudo chown -R www-data:www-data /var/www/html/your-site
```

## 2. Folders: 755

```bash
sudo find /var/www/html/your-site -type d -exec chmod 755 {} \;
```

## 3. Files: 644

```bash
sudo find /var/www/html/your-site -type f -exec chmod 644 {} \;
```

## 4. Lock down wp-config.php

```bash
sudo chmod 640 /var/www/html/your-site/wp-config.php
```

## 5. Make sure uploads is writable

```bash
sudo chown -R www-data:www-data /var/www/html/your-site/wp-content/uploads
sudo find /var/www/html/your-site/wp-content/uploads -type d -exec chmod 755 {} \;
sudo find /var/www/html/your-site/wp-content/uploads -type f -exec chmod 644 {} \;
```

## 6. Local development only: give your user write access

On a local machine, you can add your own Linux user to the `www-data` group so you can edit files without `sudo`. Don't use these looser permissions on a live server.

```bash
sudo usermod -a -G www-data <your-user>
newgrp www-data
sudo find /var/www/html/your-site -type d -exec chmod 775 {} \;
sudo find /var/www/html/your-site -type f -exec chmod 664 {} \;
```

## 7. Stop the FTP credentials prompt

Add this to `wp-config.php`, above the "That's all, stop editing!" line:

```php
define( 'FS_METHOD', 'direct' );
```

## 8. Restart the web server

```bash
sudo systemctl restart apache2
# or
sudo systemctl restart nginx
```

## 9. Check it works

- Upload an image in **Media → Add New**
- Install a plugin in **Plugins → Add New**
- Open an uploaded file in the browser, e.g. `http://localhost/your-site/wp-content/uploads/test.jpg`

## Quick version (run from the site's root folder)

```bash
sudo chown -R www-data:www-data .
sudo find . -type d -exec chmod 755 {} \;
sudo find . -type f -exec chmod 644 {} \;
```
