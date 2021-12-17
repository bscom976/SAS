# 1.ansible

Buat file sublaravel di file ansible laravel
![1](https://github.com/bscom976/SAS/blob/9956869fe0c532adf0e02d82259cc9cca4c5290f/modul3/modul%203/1.jpg)

isi dile sublaravel
```
---
- hosts: all
  become : yes
  tasks:
    - name: install bind9 dan dnsutils
      apt:
       pkg:
         - bind9
         - dnsutil
```
![3](https://github.com/bscom976/SAS/blob/80a44eb6c1681f1779fb76177449a2ee95a97ed4/modul3/modul%203/sublaravel.jpg)

install dengan ```ansible-playbook -i host sublaravel.yml -k
![2](https://github.com/bscom976/SAS/blob/9956869fe0c532adf0e02d82259cc9cca4c5290f/modul3/modul%203/2.jpg)

buat file confi.yml
![4](https://github.com/bscom976/SAS/blob/80a44eb6c1681f1779fb76177449a2ee95a97ed4/modul3/modul%203/confi.jpg)

```
---
- hosts: all
  become : yes
  tasks:
   - name: membuat direktori
     file:
      path: /var/www/html/dev/landing
      state: directory
   - name: copy file vm.local
     copy:
      src: /etc/bind/vm/vm.local
      dest: /var/www/html/dev/landing
   - name: mengganti konfigurasi
     replace:
      path: /var/www/html/dev/landing/vm.local
      regexp: 'www'
      replace: 'dev'
   - name: copy file named.conf.local
     copy:
      src: /etc/bind/named.conf.local
      dest: /etc/bind/named.conf.local
   - name: mengganti konfigurasi conf local
     replace:
      path: /etc/bind/named.conf.local
      regexp: '/etc/bind/vm/vm.local'
      replace: '/var/www/html/dev/landing/vm.local'
   - name: mengganti konfigurasi conf local part2
     replace:
      path: /etc/bind/named.conf.local
      regexp: '/etc/bind/vm/21.168.192.in-addr.arpa'
      replace: '/var/www/html/dev/landing/21.168.192.in-addr.arpa'
   - name: copy file 21.168.192.in-addr.arpa
     copy:
      src: /etc/bind/vm/21.168.192.in-addr.arpa
      dest: /var/www/html/dev/landing
   - name: copy file resolv.conf
     copy:
      src: /etc/resolv.conf
      dest: /etc/resolv.conf
   - name: copy file named.conf.options
     copy:
      src: /etc/bind/named.conf.options
      dest: /etc/bind/named.conf.options
   - name: restart nginx
     service:
      name: nginx
      state: restarted
   - name: restart bind9
     action: service name=bind9 state=restarted
```
install menggunakan ``` ansible-playbook```
![5](https://github.com/bscom976/SAS/blob/80a44eb6c1681f1779fb76177449a2ee95a97ed4/modul3/modul%203/3.jpg)

Add subdomain to /etc/hosts

![7](https://github.com/bscom976/SAS/blob/c9a775cf6dd1f3a1241ccb937f20455350562db0/modul3/modul%203/hosts.jpg)

Tambah garis ``` wwww ``` di vm.local ubuntu_landing
![6](https://github.com/bscom976/SAS/blob/80a44eb6c1681f1779fb76177449a2ee95a97ed4/modul3/modul%203/4.jpg)

buka dan edit vm.local di ``` /etc/nginx/sites-enabled/vm.local ```
```
nano /etc/nginx/sites-enabled/vm.local
```

![11](https://github.com/bscom976/SAS/blob/c9a775cf6dd1f3a1241ccb937f20455350562db0/modul3/modul%203/vm.local.jpg)

buka dan edit vm.local in directory ```/etc/bind/vm/``` dengan nenambahkan dev 
![p](https://github.com/bscom976/SAS/blob/c9a775cf6dd1f3a1241ccb937f20455350562db0/modul3/modul%203/binvm.local.jpg)

![a](https://github.com/bscom976/SAS/blob/c9a775cf6dd1f3a1241ccb937f20455350562db0/modul3/modul%203/restart2.jpg)

![e](https://github.com/bscom976/SAS/blob/c9a775cf6dd1f3a1241ccb937f20455350562db0/modul3/modul%203/Status.jpg)

ubah dns pc ke ip kita
![dbs](https://github.com/bscom976/SAS/blob/c9a775cf6dd1f3a1241ccb937f20455350562db0/modul3/modul%203/DNS%20ip4.jpg)

buka di browser
![wq](https://github.com/bscom976/SAS/blob/3981f7109fdbfec4ef0fdd69a7e2c3e6bcc3e6e9/modul3/modul%203/vm.jpg)

karena tidak bisa dibuka tidak tau masalahnya apa

