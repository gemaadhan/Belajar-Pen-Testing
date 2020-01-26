# Ganti MAC ADDRESS
```
ifconfig wlan0 down 
ifconfig wlan0 hw ether 00:11:22:33:44:55
ifconfig wlan0 up
```

mac address akan balik lagi habis di reboot. karena perubahan hanya di simpan di memory. mac address ga akan kembali ke default selama ngga di reboot, kalo itu terjadi berarti ada problem.

# Ubah mode
untuk melihat mode yang sedang aktif pada wireless adapter, masukkan command `iwconfig`. mode default adalah mode managed, mode ini hanya akan menangkap trafik yang dest mac address nya adalah dest address wireless adapter kita. 

agar bisa menangkap seluruh trafik yang lewat, kita perlu merubah menjadi mode monitor. namun sebelum nya kita perlu mematikan service yang mungkin akan mengganggu saat kita menyalakan mode ini. 
```
airmon-ng check kill
```

command di atas akan mengkill otomatis proses proses yang mungkin akan menggangu saat kita menggunakan mode monitor. 

setelah itu baru kita bisa menyalakan mode monitor dengan cara 
```
ifconfig wlan0 down
iwconfig wlan0 mode monitor
ifconfig wlan0 up 
```

Ketika monitor mode sudah aktif kita bisa mengcapture semua paket yang dikirim dalam jangkuan kita, bahkan jika paket tidak ditujukan untuk komputer kita, bahkan kita tidak terhubung ke target network, bahkan tanpa mengetahui password target network kita. semua itu dilakukan dengan paket sniffer bernama airodump-ng.

![logo]:https://github.com/gemaadhan/Belajar-Pen-Testing/blob/master/Assets/AIRODUMP-NG%20WLAN0.png
