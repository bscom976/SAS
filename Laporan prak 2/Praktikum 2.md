# Kelompok 2

## 1. Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)

cek cointrainers menggunakan ```lxc-ls -f```
![1](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/1.jpg)

hapus ubuntu_landing dan buat ubuntu focel baru dengan ```lxc-create```
```
sudo lxc-destroy ubuntu_landing
```
![1.1](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/2.jpg)

command lxc-create
```
sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```
![2](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/3.jpg)

start ubuntu landing dan masuk ke dalam ubuntu landing
 ```
 sudo lxc-start -n ubuntu_landing
 sudo lxc-attach -n ubuntu_landing
 ```
![3](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/4.jpg)
 
install nano pada ubuntu_landing

![4](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/5.jpg)

Atur ip ubuntu_landing
```
sudo nano /etc/netplan/10-lxc.yaml
```
![6](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/6.jpg)

setting ubuntu_landing auto start

![auto](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/Auto%20start.jpg)

install ssh server
```
apt install openssh-server -y
```
![7](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/7.jpg)

masuk ke ```/etc/ssh/sshd_config``` dan tambahan code dibawah dan jalankan ```service sshd restart```
```
PermitRootLogin yes
RSAAuthentication yes
```
![8](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/8.jpg)

cek ssh

![9](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/9.jpg)

## 2. Rubah LXC php7 dengan ubuntu focal (destroy n create, same ip, same name)

cek lxc, dan hapus ubuntu_php7.4

![10](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/10.jpg)

Buat ubuntu_php7.4
```
sudo lxc-create -n ubuntu_php7 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```
![11](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/11.jpg)

start ubuntu_php7 dan masuk ke dalam ubuntu php7
```
sudo lxc-start -n ubuntu_php7
sudo lxc-attach -n ubuntu_php7
```
![12](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/12.jpg)

install nano

setting ip 

![13](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/13.jpg)

setting auto start

![auto](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/Auto%20start%20php7.jpg)

install ssh

![14](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/14.jpg)

config ssh

![15](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/15.jpg)

cek ssh

![16](https://github.com/bscom976/SAS/blob/ca40c91619fb8a7a4fde0cae0d0a718b99df831f/Laporan%20prak%202/asset/16.jpg)
