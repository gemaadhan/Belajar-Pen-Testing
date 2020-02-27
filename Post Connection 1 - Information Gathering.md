# POST CONNECTION

## INFORMATION GATHERING
IP, MAC, OS, Port, Service. bisa dilakukan ketika kita sudah terhubung kejaringan. salah satu tool yang bisa digunakan adalah netdiscover

```
#netdiscover -r 10.0.2.1/24
```

## BASIC NMAP
`zenmap` adalah gui dari nmap. jika kita ga apal command nmap, di dalam zenmap disediakan beberapa profile yang siap pakai. 

### PING SCAN PROFILE
sometimes beberapa device ga bisa di ping, walaupun sebenarnya mereka up. maka hasil nya tidak akan muncul di `ping scan` nmap. setelah command di jalankan akan muncul informasi mengenai mac, ip dan vendor dari sana kita bisa mengira ngira os apa yang digunakan, misal HTC berarti osnya mungkin android, apple mungkin menggunakan ios atau mac os, dst.

### QUICK SCAN
hasil yang di dapat sama dengan `ping scan` tapi dengan `quick scan` profile kita bisa melihat port apa saja yang open pada target. 

### QUICK SCAN PLUS
dengan profile ini, kita akan mendapat informasi lebih detail tentang, versi service yang digunakan, os apa yang digunakan, device apa yang digunakan. sehingga kita bisa mencari vulnerability dari service version yang kita dapatkan. 

#### FACTS
ketika iphone di jailbreak, defaulnya port 22 nya akan kebuka dengan user root dan password alpine. 






