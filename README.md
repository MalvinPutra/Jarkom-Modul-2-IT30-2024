# Jarkom-Modul-2-IT30-2024

**KELOMPOK IT18**
| Nama | NRP |
|---------------------------|------------|
|Riskiyatul Nur Oktarani | 5027231013 |
|Malvin Putra Rismahardian | 5027231048 |

<hr>

### Topologi IT30

![image](https://github.com/user-attachments/assets/39e9e4d0-0dd0-4b50-9b85-1db27af4b6ef)



**Soal 1**

Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave.

**ROUTER**

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.248.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.248.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.248.3.1
	netmask 255.255.255.0

```


**Sanjaya**

```
auto eth0
iface eth0 inet static
   address 192.248.1.2
   netmask 255.255.255.0
   gateway 192.248.1.1

```

**Sriwijaya**

```
auto eth0
iface eth0 inet static
   address 192.248.1.3
   netmask 255.255.255.0
   gateway 192.248.1.1

```

**Tanjungkulai**

```
auto eth0
iface eth0 inet static
   address 192.248.1.4
   netmask 255.255.255.0
   gateway 192.248.1.1

```

**Bedahulu**

```
auto eth0
iface eth0 inet static
   address 192.248.1.5
   netmask 255.255.255.0
   gateway 192.248.1.1

```

**Solok**

```
auto eth0
iface eth0 inet static
   address 192.248.3.2
   netmask 255.255.255.0
   gateway 192.248.3.1

```

**Majapahit**

```
auto eth0
iface eth0 inet static
   address 192.248.2.2
   netmask 255.255.255.0
   gateway 192.248.2.1

```

**Jayanagara**

```
auto eth0
iface eth0 inet static
   address 192.248.2.4
   netmask 255.255.255.0
   gateway 192.248.2.1

```

**Kotalingga**

```
auto eth0
iface eth0 inet static
   address 192.248.2.5
   netmask 255.255.255.0
   gateway 192.248.2.1

```

**Anusapati**

```
auto eth0
iface eth0 inet static
   address 192.248.2.6
   netmask 255.255.255.0
   gateway 192.248.2.1

```

- yang pertama yaitu mencari nameserver di nusantara, menggunakan command berikut, sehingga mendapat nameserver 192.168.122.1

  ```
  cat /etc/resolv.conf
  ```

- setelah itu kita install bind9 di sriwijaya
  
- selanjutnya yaitu menggunakan command berikut di nusantara
  
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.248.0.0/16
```

- selanjutnya yaitu melakukan tes PING

![image](https://github.com/user-attachments/assets/ccf082cc-c37d-4a38-8cef-00e89c0c64ba)

![image](https://github.com/user-attachments/assets/d1a097a9-b7d2-429b-b346-5fbdc879a9b0)

### Soal 2

Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.

- pertama yaitu menggunakan command berikut untuk menambahkan ip sriwijaya

```
nano /etc/resolv.conf
```

```
nameserver 192.248.1.3
```

- selanjutnya yaitu memasukkan script ke dalam /root/.bashrc

```
nano /root/.bashrc
```

```
#!/bin/bash

echo 'zone "sudarsana.it30.com" {
	type master;
	file "/etc/bind/jarkom/sudarsana.it30.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/sudarsana.it30.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it30.com. sudarsana.it30.com. (
                        2024100121      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it30.com.
@       IN      A        192.248.3.2    ; IP Solok
www     IN      CNAME   sudarsana.it30.com.' > /etc/bind/jarkom/sudarsana.it30.com

service bind9 restart
```

- selanjutnya uji coba ping di sriwijaya

```
ping sudarsana.it30.com
```

![WhatsApp Image 2024-10-04 at 01 21 34_d33d1bda](https://github.com/user-attachments/assets/b1b60efc-9791-4cc6-91b6-20632ad10105)

### Soal 3

Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.

- masukan script ke root/.bashrc menggunakan nano

```
#!/bin/bash

echo 'zone "pasopati.it30.com" {
	type master;
	file "/etc/bind/jarkom/pasopati.it30.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/pasopati.it30.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it30.com. pasopati.it30.com. (
                        2024100121      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it30.com.
@       IN      A       192.248.2.4     ; IP Kotalingga
www     IN      CNAME   pasopati.it30.com.' > /etc/bind/jarkom/pasopati.it30.com

service bind9 restart
```

- coba ping

```
ping pasopati.it30.com
```

![WhatsApp Image 2024-10-04 at 01 28 41_23d9d13f](https://github.com/user-attachments/assets/89e9844c-1856-4eb8-857d-7917217967a7)

### Soal 4

Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com. Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.

- sama seperti nomer 2 dan 3 yaitu memasukkan script ke /root/.bashrc

  ```
  #!/bin/bash

echo 'zone "rujapala.it30.com" {
	type master;
	file "/etc/bind/jarkom/rujapala.it30.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/rujapala.it30.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     rujapala.it30.com. rujapala.it30.com. (
                        2024100121      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      rujapala.it30.com.
@       IN      A       192.248.1.4     ; IP Tanjungkula
www     IN      CNAME   rujapala.it30.com.' > /etc/bind/jarkom/rujapala.it30.com

service bind9 restart
```

- coba ping

```
ping rujapala.it30.com
```

![WhatsApp Image 2024-10-04 at 01 32 17_76924b30](https://github.com/user-attachments/assets/b05597ce-c074-4665-8703-148cc2d0d370)

### Soal 5

Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.

- mencoba ping ke server sudarsana.it30.com , pasopati.it30.com , rujapala.it30.com dalam anusapati, sanjaya, dan jayanegara (client)

```
ping -c 2 sudarsana.it30.com
```

```
ping -c 2 pasopati.it30.com
```

```
ping -c 2 rujapala.it30.com
```

ANUSAPATI

![WhatsApp Image 2024-10-04 at 01 39 28_22c246ce](https://github.com/user-attachments/assets/4a640f41-6171-43e2-8568-93371d66c4d5)

SANJAYA

![WhatsApp Image 2024-10-04 at 01 35 40_8853b02c](https://github.com/user-attachments/assets/2d0195a7-a953-48a2-b842-d547543ec9fc)

JAYANEGARA

![WhatsApp Image 2024-10-04 at 01 37 41_220458ea](https://github.com/user-attachments/assets/48a85c87-f205-4a60-986d-61178ea53f98)

### Soal 6

Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).

### Soal 7

Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Tanjungkulai untuk semua domain yang sudah dibuat sebelumnya.

### Soal 8

Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.

- masukkan script dibawah ini ke /root/.bashrc di sriwijaya

```
#!/bin/bash
apt update
apt install bind9 -y

echo 'zone "sudarsana.it30.com" {
	type master;
	file "/etc/bind/jarkom/sudarsana.it30.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/sudarsana.it30.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it30.com. root.sudarsana.it30.com. (
                        2024100318      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it30.com.
@         IN      A       192.248.3.2     ; IP Solok
www     IN      CNAME   sudarsana.it30.com.
cakra    IN      A       192.248.1.5     ; IP Bedahulu
www     IN      CNAME   cakra.sudarsana.it30.com.' > /etc/bind/jarkom/sudarsana.it30.com
```

- lalu mencoba ping menggunakan client anusapati

```
ping cakra.sudarsana.it30.com
```

```
ping www.cakra.sudarsana.it30.com
```

![WhatsApp Image 2024-10-04 at 02 25 07_c293583d](https://github.com/user-attachments/assets/3971d058-7f4d-46a2-a6e8-0b8e4370d337)

### Soal 9

Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Tanjungkulai dengan alamat IP menuju radar di Kotalingga.

- masukkan script dibawah ini ke /root/.bashrc di sriwijaya

```
#!/bin/bash


echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it30.com. root.pasopati.it30.com. (
                        2024100319                   ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@         IN      NS      pasopati.it30.com.
@         IN      A       192.248.2.4    ; IP Kotalingga
www     IN      CNAME   pasopati.it30.com.
panah   IN      A       192.248.2.2     ; Delegasikan ke Majapahit
ns1       IN      A       192.248.2.2    ; Delegasikan ke Majapahit
panah   IN      NS      ns1' > /etc/bind/jarkom/pasopati.it30.com

echo '
options {
        directory "/var/cache/bind";

        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```

- command dibawah untuk tes ping

```
ping panah.pasopati.it30.com
```

```
ping www.panah.pasopati.it30.com
```

SANJAYA

![WhatsApp Image 2024-10-04 at 02 32 52_ab3f9830](https://github.com/user-attachments/assets/bbf7283d-ad63-4c52-8685-b1d71b4db5b9)

ANUSAPATI

![WhatsApp Image 2024-10-04 at 02 34 13_5ca7a979](https://github.com/user-attachments/assets/9d026a6a-4c1d-4713-87c2-9605fe839e52)
