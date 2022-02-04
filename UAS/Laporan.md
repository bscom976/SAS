# Tugas Akhir
Kelompok 2 

1202190010 Aditya Yudhistira 

1202199008 Bagus Setiawan 

1202190056 Ricky Darmawan

### Create lxc
![1](https://github.com/bscom976/SAS/blob/091baf9669571ec0369e55d92168c79502b059d3/UAS/Asset/Lxc.jpg)

create file Ceria in ansible ```mkdir nama file```
![2](https://github.com/bscom976/SAS/blob/091baf9669571ec0369e55d92168c79502b059d3/UAS/Asset/folder.jpg)

setting hosts for ansible 
```
127.0.0.1 localhost
127.0.1.1 kelompok2
127.0.1.1 kelompok2.fpsas news.kelompok2.fpsas


10.0.3.100 lxc_mariadb.dev
10.0.3.101 lxc_php7_1.dev
10.0.3.102 lxc_php7_2.dev
10.0.3.103 lxc_php7_3.dev
10.0.3.104 lxc_php7_4.dev
10.0.3.105 lxc_php7_5.dev
10.0.3.106 lxc_php7_6.dev
10.0.3.151 lxc_php5_1.dev
10.0.3.152 lxc_php5_2.dev


# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

```
![hosts](https://github.com/bscom976/SAS/blob/eec7c921aa458f43f650b2ff40cccbff456acc6c/UAS/Asset/hosts.jpg)


setting Hosts in ansible
```
[ci]
lxc_php5_1 ansible_host=lxc_php5_1.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php5_2 ansible_host=lxc_php5_2.dev ansible_ssh_user=root ansible_become_pass=ITTS

[laravel]
lxc_php7_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_3 ansible_host=lxc_php7_3.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_4 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_5 ansible_host=lxc_php7_5.dev ansible_ssh_user=root ansible_become_pass=ITTS

[wordpress]
lxc_php7_1 ansible_host=lxc_php7_1.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_4 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_6 ansible_host=lxc_php7_6.dev ansible_ssh_user=root ansible_become_pass=ITTS

[yii]
lxc_php7_1 ansible_host=lxc_php7_1.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_4 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_5 ansible_host=lxc_php7_5.dev ansible_ssh_user=root ansible_become_pass=ITTS
lxc_php7_6 ansible_host=lxc_php7_6.dev ansible_ssh_user=root ansible_become_pass=ITTS

[database]
lxc_mariadb ansible_host=lxc_mariadb.dev ansible_ssh_user=root ansible_become_pass=ITTS

```
![3](https://github.com/bscom976/SAS/blob/091baf9669571ec0369e55d92168c79502b059d3/UAS/Asset/Hosts_ansible.jpg)

create file for install maria db
``` sudo nano install-mariadb.yml ```
![4](https://github.com/bscom976/SAS/blob/091baf9669571ec0369e55d92168c79502b059d3/UAS/Asset/mariadb.jpg)
```
- hosts: database
  vars:
    username: 'kelompok2'
    password: 'ITTS'
    domain: 'lxc_mariadb.dev'
  roles:
    - db
    - pma
```

create file ``` taks/main.yml, handlers/main.yml, templates/my.cnf ``` in roles/db

file  Tasks``` main.yml```

![5](https://github.com/bscom976/SAS/blob/1dae597db2f9361f48f2ff60f410dac45d7da59e/UAS/Asset/db_tasks.png)

file handlers```main.yml```

![6](https://github.com/bscom976/SAS/blob/1dae597db2f9361f48f2ff60f410dac45d7da59e/UAS/Asset/db_handlers.png)

file templates ```my.cnf```

![7](https://github.com/bscom976/SAS/blob/1dae597db2f9361f48f2ff60f410dac45d7da59e/UAS/Asset/db_templates.png)


create file ``` taks/main.yml, handlers/main.yml, templates/pma.local  in roles/pma

file  Tasks``` main.yml```

![9](https://github.com/bscom976/SAS/blob/1dae597db2f9361f48f2ff60f410dac45d7da59e/UAS/Asset/PMA_tasks.png)

file handlers```main.yml```

![10](https://github.com/bscom976/SAS/blob/1dae597db2f9361f48f2ff60f410dac45d7da59e/UAS/Asset/PMA_handlers.png)

file templates ```pma.local```

![11](https://github.com/bscom976/SAS/blob/1dae597db2f9361f48f2ff60f410dac45d7da59e/UAS/Asset/PMA_templates.png)

cek in browser

![php](https://github.com/bscom976/SAS/blob/5f8a694891ac6602e7469181f643e2a45e4bf35e/UAS/Asset/Phpmyadmin.jpg)

![php1](https://github.com/bscom976/SAS/blob/5f8a694891ac6602e7469181f643e2a45e4bf35e/UAS/Asset/Phpmyadmin1.jpg)

create file for install maria db
``` sudo nano install-laravel.yml ``
```
---
- hosts: laravel
  vars:
    username: 'kelompok2'
    password: 'ITTS'
    domain: "lxc_php7_2.dev"
    domain: "lxc_php7_3.dev"
    domain: "lxc_php7_4.dev"
    domain: "lxc_php7_5.dev"
  roles:
    - php
    - lv
```

setting domain 
create file  ``` kelompok2.fpsas news.kelompok2.fpsas ```
![domain](https://github.com/bscom976/SAS/blob/45eeac0dde28b1fa622d82e27bae7e2768e576d6/UAS/Asset/kelompok2fpsas.jpg)


kelompok2.fpsas
```
upstream utama {
        least_conn;
        server lxc_php7_1.dev;
        server lxc_php7_2.dev;
        server lxc_php7_4.dev;
        server lxc_php7_6.dev;
}

upstream yii {
        server lxc_php7_1.dev weight=3;
        server lxc_php7_2.dev weight=2;
        server lxc_php7_4.dev weight=4;
        server lxc_php7_5.dev weight=1;
        server lxc_php7_6.dev weight=6;
}

upstream codeigniter {
        server lxc_php5_1.dev;
        server lxc_php5_2.dev;
}


server {
        listen 80;
        listen [::]:80;

        server_name kelompok2.fpsas;

        root /var/www/html;
        index index.php index.html;

        location /app{
                rewrite /app/?(.*)$ /$1 break;
                proxy_pass http://codeigniter;
        }

        location /product {
                rewrite /product/?(.*)$ /$1 break;
                proxy_pass http://yii;
        }

        location /phpmyadmin{
                rewrite /phpmyadmin/?(.*)$ /$1 break;
                proxy_pass http://lxc_mariadb.dev;
        }

        location / {
                #rewrite /?(.*)$ /$1 break;
                proxy_pass http://utama;
        }
}
```
news.kelompok2.fpsas

```
upstream wordpress {
        ip_hash;
        server lxc_php7_2.dev;
        server lxc_php7_3.dev;
        server lxc_php7_4.dev;
        server lxc_php7_5.dev;
}

server {
        listen 80;
        listen [::]:80;

        server_name news.kelompok2.fpsas;

        root /var/www/html;
        index index.html;

        location / {
                #rewrite /?(.*)$ /$1 break;
                proxy_pass http://wordpress;
        }
}
```
