# WIRESHARK
untuk menggunakan wireshark dan mendapatkan trafik target, kita harus menjadi man in the middle, karena secara default wireshark akan hanya melakukan sniffing pada interface milik komputer kita dimana trafik yang datang dan pergi adalah trafik untuk dan dari komputer kita. 

dengan menjadi mitm, trafik target akan dipaksa melewati interface kita sehingga kita dapat mensnif seluruh trafik target. 

untuk mencari target sedang search apa, cari method GET /search, untuk mencari user dan password kata kuncinya adalah method POST. 

karena wireshark akan menangkap semua data, presentasi admin dan password ditemukan lebih besar dibanding hanya berpatokan pada hasil bettercap. 

ketika kita tidak bisa menggunakan wireshark, misalkan kita hanya punya hp, kita bisa setting output bettercap dengan, `set net.sniff.output namafile.cap`, nanti file itu bisa dibuka untuk di analisi lebih lanjut dengan wireshark. 

kita bisa menggunakan ctrl f pada wireshark untuk mencari spesifik kata, rubah menjadi `packet list narrow & wide dan string` untuk mencari text tertentu. 