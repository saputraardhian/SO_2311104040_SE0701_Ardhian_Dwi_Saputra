# <h1 align="center">Laporan Praktikum Modul XI <br> Memori Xinu</h1>
<p align="center">Fajar Budiawan - 2311104039</p>

## Dasar Teori

Memori pada program C/C++ merupakan bagian penting yang digunakan untuk menyimpan instruksi dan data selama program dijalankan. Sistem operasi membagi memori program ke dalam beberapa segmen agar pengelolaan data menjadi lebih teratur dan efisien. Segmen tersebut terdiri dari code segment, data segment, stack segment, dan heap segment. Code segment digunakan untuk menyimpan instruksi program, data segment menyimpan variabel global dan static, stack digunakan untuk variabel lokal dan pemanggilan fungsi, sedangkan heap digunakan untuk alokasi memori secara dinamis saat program berjalan.

Pada bahasa C/C++, setiap segmen memori memiliki fungsi dan karakteristik yang berbeda. Stack memiliki proses alokasi yang cepat namun kapasitasnya terbatas, sedangkan heap memiliki kapasitas lebih fleksibel tetapi pengelolaannya harus dilakukan secara manual menggunakan new/delete atau malloc/free. Pemahaman mengenai segmen memori sangat penting bagi programmer karena berpengaruh terhadap efisiensi program, penggunaan sumber daya, serta pencegahan kesalahan seperti stack overflow dan memory leak. Dengan memahami cara kerja segmen memori, programmer dapat membuat program yang lebih optimal dan stabil.

## Jurnal

## 1.
Buatlah perintah baru bernama freememory yang memiliki dua fungsi berikut:

a. menampilkan seluruh free memory block yang tercatat dalam free memory list pada xinu

![alt text](images1.png)
![alt text](images2.png) 

b. Analisis

Perintah freememory berhasil menampilkan seluruh free memory block yang terdapat pada free memory list di Xinu. Setiap block menampilkan alamat memori, ukuran dalam bentuk desimal, dan ukuran dalam bentuk hexadecimal. Program juga menghitung total keseluruhan free memory yang masih tersedia pada sistem.

## 2. 
Jawablah pertanyaan berikut:

a. Mengapa Xinu memisahkan data segment dan BSS segment? b. Bagaimana alokasi dan dealokasi memori selama eksekusi memengaruhi ukuran free space? c. Mengapa penggunaan heap lebih berpotensi menimbulkan masalah dibandingkan stack? d. Mengapa Xinu menggunakan struktur linked list untuk menyimpan free block? e. Apa tantangan utama dalam penggunaan heap di Xinu?

Jawab :
a. Xinu memisahkan data segment dan BSS segment agar pengelolaan memori lebih rapi dan efisien. Data segment digunakan untuk menyimpan variabel global atau static yang sudah memiliki nilai awal, sedangkan BSS segment digunakan untuk variabel global atau static yang belum diberi nilai awal atau bernilai nol. Dengan pemisahan ini, sistem tidak perlu menyimpan semua nilai nol ke dalam file program, sehingga ukuran program menjadi lebih kecil dan proses inisialisasi memori lebih mudah.

b. Saat terjadi alokasi memori, sebagian ruang kosong akan digunakan oleh proses, sehingga ukuran free space berkurang. Sebaliknya, saat terjadi dealokasi memori, memori yang sudah tidak dipakai akan dikembalikan ke daftar memori kosong sehingga free space bertambah. Namun, jika alokasi dan dealokasi dilakukan berulang dengan ukuran yang berbeda-beda, dapat terjadi fragmentasi, yaitu memori kosong terpecah menjadi beberapa bagian kecil.

c. Heap lebih berpotensi menimbulkan masalah karena penggunaannya bersifat dinamis dan harus dikelola dengan hati-hati. Jika memori yang sudah dipakai tidak dikembalikan, maka dapat terjadi memory leak. Selain itu, heap juga dapat mengalami fragmentasi, kesalahan pointer, atau penggunaan memori yang sudah dibebaskan. Berbeda dengan stack yang bekerja lebih teratur karena mengikuti urutan pemanggilan fungsi dan otomatis dilepas setelah fungsi selesai.

d. Xinu menggunakan struktur linked list karena free block memiliki ukuran dan alamat yang berbeda-beda. Dengan linked list, setiap blok memori kosong dapat dihubungkan menggunakan pointer tanpa harus berada pada lokasi yang berurutan. Struktur ini memudahkan Xinu dalam menambah, menghapus, mencari, dan menggabungkan blok memori kosong saat proses alokasi atau dealokasi dilakukan.

e. Tantangan utama penggunaan heap di Xinu adalah menjaga agar memori tetap efisien dan tidak mengalami kerusakan selama proses alokasi dan dealokasi. Masalah yang dapat terjadi antara lain fragmentasi memori, memory leak, pointer yang salah, serta kesulitan menggabungkan kembali blok memori kosong. Jika heap tidak dikelola dengan baik, sistem dapat kekurangan memori meskipun sebenarnya masih ada ruang kosong yang tersebar.