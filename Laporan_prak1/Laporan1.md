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

Kemudian apply
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

### 3. setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

jalankan contrainers debian_php5.6 dan masuk ke debian_php5.6
```
sudo lxc-start -n debian_php5.6
sudo lxc-attach -n debian_php5.6
```
![msk](https://github.com/bscom976/SAS/blob/1eb8cbb0da9b7cc3b541586d96c39620313fca32/Laporan_prak1/Asset/Msuk%20debian.jpg)

Install nginx
```
sudo apt install nginx nginx-extras
```
![nginx](https://github.com/bscom976/SAS/blob/a3ad66ae2fe94467bdafcd3e233f5ace1a3244c4/Laporan_prak1/Asset/nginx.jpg)

install tools
```
sudo apt install nano net-tools curl
```
![tools](https://github.com/bscom976/SAS/blob/3739e285deeec32f05bb0222c6d70b3d746a1765/Laporan_prak1/Asset/tools.jpg)

ubah Ip ke 10.0.3.102

source :
```
nano /etc/network/interfaces
```
![ipdebian](https://github.com/bscom976/SAS/blob/cf8a2f60602bf14d02b1f220ad6305efcb9773fa/Laporan_prak1/Asset/ubah%20ip%20debian.jpg)

restart debian dan cek Ip 
```
sytemctl restart networking.service
ifconfig
exit
sudo lxc-ls -f
```
![ceki](https://github.com/bscom976/SAS/blob/189282430e32e530e6b8140fe40faf1b2ed27eb8/Laporan_prak1/Asset/restart.jpg)

bila alamat ip double reboot
```
reboot
```
![re](https://github.com/bscom976/SAS/blob/85cfc4786badefb98474075aef16b0dcac0a9226/Laporan_prak1/Asset/reboot.jpg)

setting nginx dan buat file lxc_php5.6.dev
```
cd /etc/nginx/sites-available
touch lxc_php5.6.dev
nano lxc_php5.6.dev
```
![set](https://github.com/bscom976/SAS/blob/da29fc91e7e42cb3d433dc16ed984179b78e608f/Laporan_prak1/Asset/Buat%20file.jpg)

konfigurasi

![konf](https://github.com/bscom976/SAS/blob/ac001c457fbdf81b4b78c7bc74cd850f8537dad3/Laporan_prak1/Asset/konfigurasi%20debian.jpg)

masuk ke sites-enabled
```
cd ../sites-enabled
ln -s /etc/nginx/sites-available/lxc_php5.6.dev
```
![enap](https://github.com/bscom976/SAS/blob/ab2fcb83418f51def5a60bb6a3f7de35a4b3b63a/Laporan_prak1/Asset/Sites%20enabled.jpg)

masuk ke hots dan konfigurasi menambahakan lxc_php5.6.dev
```
nano /etc/hosts
```
![msk+host](https://github.com/bscom976/SAS/blob/a0569e53798ef41734885e5123180dbbd17807b5/Laporan_prak1/Asset/hosts.jpg)

![+hosts](https://github.com/bscom976/SAS/blob/a0569e53798ef41734885e5123180dbbd17807b5/Laporan_prak1/Asset/hosts%202.jpg)

masuk ke direktori html 
```
cd /var/www/html
mkdir lxc_php5.6
cp index.nginx-debian.html lxc_php5.6/index.html
nano lxc_php5.6/index.html
```
![Html](https://github.com/bscom976/SAS/blob/13c08774ac1608c5b993756fd21788c260c8efb7/Laporan_prak1/Asset/index.html.jpg)

![HTML](https://github.com/bscom976/SAS/blob/ee298790e525ada8d7485d7a1e349f03500fdf32/Laporan_prak1/Asset/HTML.jpg)

### 4. Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc

Setting file lxc_landing seperti dibawah 
![landinf](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/lxc_landing.jpg)

tambah lxc_landing.dev pada hosts

![lanhosts](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/Host.jpg)

masuk ke direktori html

![1](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/direktori%20html.jpg)
![2](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/html.jpg)

### 5. LXC ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website company profile tidak mengalami downtime
Stop ubuntu_landing
```
sudo stop -n ubuntu_landing
```
![stopq](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/Stop.jpg)
masuk ke ubuntu_landing
```
sudo su
cd /var/lib/lxc
cd ubuntu_landing
```
![sudosu](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/sudo.jpg)

kemudian pergi ke config lalu tambahkan ```lxc.start.auto = 1 ```
```
nano config
lxc.start.auto = 1
```
![nanoconfig](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/config.jpg)
![auto](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/ubuntu_landing.jpg)

reboot dan cek
```
reboot
sudo lxc-ls -f
```
![Reboot](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/Reboot.jpg)
![Lxc-ls](https://github.com/bscom976/SAS/blob/eae1f155b93a81d9022a6ea24b769e6c0b5cdfdf/Laporan_prak1/Asset/Ubuntu%20landing%20setting/cek.jpg)

### 6. Setup nginx pada vm.local untuk mengatur proxy_pass
masuk ke host vm.local
```
sudo nano /etc/hosts
```
![vm.local](https://github.com/bscom976/SAS/blob/11d44830895982100cea274cd89c461f1b64c37f/Laporan_prak1/Asset/Proxy/Host.jpg)

masuk ke direktori sites-available, lalu masuk ke vm.local

![sites-av](https://github.com/bscom976/SAS/blob/11d44830895982100cea274cd89c461f1b64c37f/Laporan_prak1/Asset/Proxy/Sites.jpg)

Setingg sepeti gamabar dibawah

![set](https://github.com/bscom976/SAS/blob/11d44830895982100cea274cd89c461f1b64c37f/Laporan_prak1/Asset/Proxy/vm.local.jpg)

### 7. untuk kebutuhan presentasi mereka, browser di laptop mereka harus dapat mengakses ketiga url tersebut.

cek di browser
![vm](https://github.com/bscom976/SAS/blob/02c944d8a9e3a3fa73ca3b0348a80b6ca7766503/Laporan_prak1/Asset/Proxy/Website/Vm.local.jpg)

![blog](https://github.com/bscom976/SAS/blob/02c944d8a9e3a3fa73ca3b0348a80b6ca7766503/Laporan_prak1/Asset/Proxy/Website/blog.jpg)

![app](https://github.com/bscom976/SAS/blob/02c944d8a9e3a3fa73ca3b0348a80b6ca7766503/Laporan_prak1/Asset/Proxy/Website/app.jpg)

sever tidak bisa di akses dan tidak tau penyebabnya

### 8. Analisis Praktikum
#### *mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9
karena ubuntu 16.04 sudah tidak di support oleh sistem, update ubuntu 16.04 terakhir pada april 2021 kemarin,
sedangan debian bisa di support oleh sistem sampai dengan tahun 2022
#### *kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop
karena virtualisasi dari lxc tegolong ringan untuk perangat dan efisien tanpa perlu perngkat lain lagi cukup satu
perangkat, biaya bisa di minimalis
#### *apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?
Proxy server (peladen proxy) adalah sebuah komputer server atau program komputer yang dapat bertindak sebagai komputer lainnya untuk melakukan request terhadap content dari Internet atau intranet. karena vm.local di konfigurasikan bisa mengakses web yang ada di komputer server, walupun praktikum konfigurasinya gagal dan tidak bisa tersambung ke website
