# payeat-cloud-config
Migrate purpose

Nginx Config
```bash
server {
        listen 8080;
    # Log files for Debugging
        access_log /var/log/nginx/payeat-access.log;
        error_log /var/log/nginx/payeat-error.log;

    # Webroot Directory for Laravel project
        root /opt/payeat/public;
        index index.php index.html index.htm;

        # Your Domain Name
        server_name merchant.payeatpos.com;

        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }

    # PHP-FPM Configuration Nginx
        location ~ \.php$ {
                try_files $uri =404;
                fastcgi_split_path_info ^(.+\.php)(/.+)$;
                fastcgi_pass unix:/run/php-fpm/php-fpm.sock;
                fastcgi_index index.php;
                fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                include fastcgi_params;
        }
}
```
