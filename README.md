# Jarkom-Modul-2-IT30-2024

**KELOMPOK IT18**
| Nama | NRP |
|---------------------------|------------|
|Riskiyatul Nur Oktarani | 5027231013 |
|Malvin Putra Rismahardian | 5027231048 |

<hr>

### Topologi IT30

![list](https://cdn.discordapp.com/attachments/1291410724857577625/1291410753802473678/image.png?ex=66ffff7c&is=66feadfc&hm=d5480904ca0e5eff4943c0558c85b52776fb81e2bfd24b4430001a40fbaadcd3&)


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

### Soal 2

Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.
