# Домашнее задание к занятию 1 «Disaster recovery и Keepalived»

# Задание 1
Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.
На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

# Ответ.
![Скрин 1](https://github.com/MalovAleksey/DZ/blob/main/2023-11-09_09-29-46.png)
![Скрин 2](https://github.com/MalovAleksey/DZ/blob/main/2023-11-09_09-29-57.png)


# Задание 2

Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.
Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

# Ответ.

# Keepalived-script
```Bash
#!/bin/bash
 nc -vz 127.0.0.1 80 && test -s /var/www/html/index.nginx-debian.html
```
# /etc/keepalived/keepalived.conf
```Bash
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
