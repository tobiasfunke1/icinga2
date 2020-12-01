# icinga2

### change ssh port for hosts:
```
hosts.conf
object Host "hostname123" {
...
vars.ssh_port = 1023
...
}

services.conf
apply Service "ssh" {
 ...
 check_command = "ssh"
 vars.port = host.vars.ssh_port
 ...
}

[https://monitoring-portal.org/woltlab/index.php?thread/32752-ssh-monitoring-different-port/]
```
### nginx
```
server {
        listen 10.x.x.x:80;
        listen 127.0.0.1:80;
        server_name 10.x.x.x,127.0.0.1,localhost;

        location ~ ^/icingaweb2/index\.php(.*)$ {
                fastcgi_pass unix:/run/php/php7.2-fpm.sock;
                fastcgi_index index.php;
                include fastcgi_params;
                fastcgi_param SCRIPT_FILENAME /usr/share/icingaweb2/public/index.php;
                fastcgi_param ICINGAWEB_CONFIGDIR /etc/icingaweb2;
                fastcgi_param REMOTE_USER $remote_user;
        }
        location ~ ^/icingaweb2(.+)? {
                alias /usr/share/icingaweb2;
                index index.php;
                try_files $1 $uri $uri/ /icingaweb2/index.php$is_args$args;
        }
}
```
