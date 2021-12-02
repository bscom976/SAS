# Kelompok 2

## 1. Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)

cek cointrainers menggunakan ```lxc-ls -f```
![]()

hapus ubuntu_landing dan buat ubuntu focel baru dengan ```lxc-create```
```
sudo lxc-destroy ubuntu_landing
```
![]()
command lxc-create
```
sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```
![]()

start ubuntu landing dan masuk ke dalam ubuntu landing
 ```
 sudo lxc-start -n ubuntu_landing
 sudo lxc-attach -n ubuntu_landing
 ```
 ![]()
 
install nano pada ubuntu_landing
![]()

Atur ip ubuntu_landing
```
sudo nano /etc/netplan/10-lxc.yaml
```
![]()

![]()

setting ubuntu_landing auto start
![]()

install ssh server
![]()

masuk ke ```/etc/ssh/sshd_config``` dan tambahan code dibawah dan jalankan ```service sshd restart```
```

```
![]()

![]()
