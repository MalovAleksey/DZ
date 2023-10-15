# DZ 
# Keepalived-script
#!/bin/bash
 nc -vz 127.0.0.1 80 && test -s /var/www/html/index.nginx-debian.html

# /etc/keepalived/keepalived.conf
```
global_defs {
enable_script_security
}
vrrp_script nginx_check {
script "/usr/bin/keepalived-script"
interval 3
user keepalived_script
}
vrrp_instance VI_1 {
        state MASTER
        interface enp0s3
        virtual_router_id 15
        priority 250
        advert_int 1

        virtual_ipaddress {
              192.168.0.15/24
        }
track_script {
nginx_check
}
}
```
![Скрин 1](https://github.com/MalovAleksey/DZ/blob/main/2023-10-15_10-25-06.png)
![Скрин 1](https://github.com/MalovAleksey/DZ/blob/main/2023-10-15_10-25-31.png)
