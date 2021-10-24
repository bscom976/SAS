 #### 1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema yang baru

Rename ubuntu_php5.6 menjadi ubuntu_landing
 source :
 ```
 sudo lxc-copy -R -n ubuntu_php5.6 -N ubuntu_landing
 ``` 
 ![rename](https://github.com/bscom976/SAS/blob/ac1402d9356784e9fe19f8a7bd6583a326bf711c/Laporan_prak1/Asset/Ubuntu%20landing.png)
 
Start ubuntu_landing
Source :
```
sudo lxc-start -n ubuntu_landing 
sudo lxc-attach -n ubuntu_landing
```
![Start](https://github.com/bscom976/SAS/blob/ac1402d9356784e9fe19f8a7bd6583a326bf711c/Laporan_prak1/Asset/start%20Ubuntu_landing.png)

Melakukan penggantian IP address di ubuntu_landing
Source : 
```
nano /etc/network/interfaces
```
![ip](https://github.com/bscom976/SAS/blob/ac1402d9356784e9fe19f8a7bd6583a326bf711c/Laporan_prak1/Asset/pengantian%20IP%20address%20%20ubuntu_landing.png)

Setelah berhasil melakukan perubahan Ip pada ubuntu_landing, lakukan reboot
Source : 
```
reboot
```
![reboot](https://github.com/bscom976/SAS/blob/ac1402d9356784e9fe19f8a7bd6583a326bf711c/Laporan_prak1/Asset/Rehoot%20ubuntu_landing.png)

Coba test ping google
Source : 
```
ping 8.8.8.8
ping google.com
```
![ping8](https://github.com/bscom976/SAS/blob/ac1402d9356784e9fe19f8a7bd6583a326bf711c/Laporan_prak1/Asset/Ping%20ubuntu_landing.png)

Kemudian ubah ip ubuntu_php7.4
Source :
```
sudo lxc-start -n ubuntu_php7.4
sudo lxc-attach -n ubuntu_php7.4
nano /etc/netplan/10-lxc.yaml
```
![ubahip](https://github.com/bscom976/SAS/blob/af7acabba5c792b711b47e597ae8e8c29b9f3043/Laporan_prak1/Asset/ubah%20ip%20ubuntu_7.4.png)

Kemudian aplly
Source : 
```
sudo netplan apply
```
![apply](https://github.com/bscom976/SAS/blob/af7acabba5c792b711b47e597ae8e8c29b9f3043/Laporan_prak1/Asset/Apply.png)

### 2. Install lxc debian 9 dengan nama debian_php5.6

Install LXC debian 
Source :
```
sudo lxc-create -n ubuntu_php5.6 -t download -- --dist debian --release stretch --arch amd64  --no-validate --server uk.images.linuxcontainers.org
```
![instal](https://github.com/bscom976/SAS/blob/af7acabba5c792b711b47e597ae8e8c29b9f3043/Laporan_prak1/Asset/Install%20debian.png)

Kemudian cek apakah debian sudah terinstall
Source : 
```
sudo lxc-ls -f
```
![cek](https://github.com/bscom976/SAS/blob/af7acabba5c792b711b47e597ae8e8c29b9f3043/Laporan_prak1/Asset/cek%20debian.png)

