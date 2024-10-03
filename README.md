# namer_app

A new Flutter project.

## Identitas Mahasiswa

> Nama  : Triyana Dewi Fatmawati <br/>
> NIM   : 2241720206 <br/>
> Kelas : TI - 3H <br/>
> Nomor : 25 <br/>

---
### Demo Output
![Hasil Tambah Halaman Baru](/images/hasil-namer_app.gif)

## Langkah-langkah Pengerjaan
### Pendahuluan
Flutter adalah toolkit UI Google untuk membangun aplikasi untuk seluler, web, dan desktop dari satu basis kode. Dalam codelab ini, Anda akan mem-build aplikasi Flutter berikut: <br>
Aplikasi ini menghasilkan nama yang terdengar keren, seperti "newstay", "lightstream", "mainbrake", atau "graypine". Pengguna dapat menanyakan nama berikutnya, memfavoritkan nama saat ini, dan meninjau daftar nama favorit di halaman terpisah. Aplikasi ini responsif terhadap berbagai ukuran layar.

### Buat proyek Flutter
#### Modifikasi isi file
Di panel kiri VS Code, pastikan Explorer dipilih, dan buka file.pubspec.yaml. Ganti isi file ini dengan yang berikut:

![Hasil Modifikasi pubspec](/images/pubspec_yaml.png)

File menentukan informasi dasar tentang aplikasi Anda, seperti versi saat ini, dependensinya, dan aset yang akan dikirimkan.pubspec.yaml

Selanjutnya, buka file konfigurasi lain di proyek, .analysis_options.yaml. Ganti isinya dengan yang berikut:

![Hasil Modifikasi analysis_options](/images/analysis_options_yaml.png)

Terakhir, buka file di bawah direktori.main.dartlib/
Ganti isi file ini dengan yang berikut:

![Hasil Modifikasi main](/images/main_dart.png)

### Tambahkan Button
Langkah ini menambahkan tombol Next untuk menghasilkan pasangan kata baru.

- Pertama, buka lib/main.dart dan pastikan Anda telah memilih perangkat target. Di sudut kanan bawah VS Code, Anda akan menemukan button yang menunjukkan perangkat target saat ini. Klik untuk mengubahnya.
- Saat terbuka, temukan button "play" di sudut kanan atas jendela VS Code, dan klik.lib/main.dart
- Setelah sekitar satu menit, aplikasi diluncurkan dalam mode debug. Seperti berikut:
![Hasil Eksekusi 1](/images/langkah4-1.png)

#### Hot Reload Pertama
Di bagian bawah lib/main.dart, tambahkan sesuatu pada string di objek Text pertama, dan simpan file tersebut (dengan Ctrl+S atau Cmd+S). Misalnya:
![Hasil Hot Reload](/images/maindart_2.png)

Perhatikan bagaimana aplikasi segera berubah tetapi kata acak tetap sama. Ini adalah Hot Reload stateful Flutter yang terkenal di tempat kerja. Hot reload dipicu saat Anda menyimpan perubahan pada file sumber.

#### Menambahkan Button
Berikutnya, tambahkan button di bagian bawah Column, tepat di bawah instance Text kedua.
![Hasil Menambahkan Button](/images/button.png)

Saat perubahan disimpan, aplikasi diperbarui kembali: Sebuah button muncul dan, saat button tersebut diklik, Debug Console di VS Code menampilkan pesan button pressed!.
![Hasil Menambahkan Button](/images/hasil-button.png)

Meskipun menyenangkan melihat Debug Console, Anda ingin button tersebut melakukan sesuatu yang lebih berguna. Namun, sebelum mencapai ke sana, perhatikan kode pada lib/main.dart lebih dekat, untuk memahami cara kerjanya. <br>

Selanjutnya, akan menghubungkan button dengan status.
Scroll ke MyAppState lalu tambahkan metode getNext.
![Hasil Menambahkan MyAppState](/images/myappstate.png)

Selanjutnya memanggil metode getNext dari callback tombol tersebut.
![Hasil Menambahkan MyAppState](/images/callback.png)

Simpan dan uji coba aplikasi sekarang. Aplikasi akan menghasilkan pasangan kata acak baru setiap kali Anda menekan tombol Next.
![Hasil percobaan klik button](/images/hasil-callback.gif)

### Mempercantik Tampilan
#### Ekstrak Widget
Baris yang bertanggung jawab untuk menampilkan pasangan kata saat ini kini tampak seperti berikut: Text(appState.current.asLowerCase). Untuk mengubahnya menjadi sesuatu yang lebih kompleks, disarankan untuk mengekstrak baris ini ke widget terpisah. Memiliki beberapa widget untuk beberapa bagian logis dari UI Anda adalah cara penting dalam mengelola kompleksitas pada Flutter.

Flutter menyediakan pembantu pemfaktoran ulang untuk mengekstrak widget, tetapi sebelum Anda menggunakannya, pastikan bahwa baris yang akan diekstrak hanya mengakses yang diperlukan. Sekarang baris tersebut mengakses appState, tetapi sebenarnya baris tersebut hanya perlu mengetahui apa pasangan kata saat ini.

Oleh karena itu, tulis ulang widget MyHomePage sebagai berikut:
![Hasil Menambahkan Widget](/images/widget.png)

Bagus. Widget Text tidak lagi merujuk kepada keseluruhan appState.

Sekarang, panggil menu Refactor. Pada VS Code, lakukan salah satu dari dua cara:

1. Klik kanan potongan kode yang ingin difaktorkan ulang (dalam hal ini Text) dan pilih Refactor... dari menu drop-down, <br>
ATAU <br>
2. Pindahkan kursor Anda ke potongan kode yang ingin Anda faktorkan ulang (dalam hal ini, Text), lalu tekan Ctrl+. (Win/Linux) <br>
![Hasil Menambahkan Widget](/images/widget-bigcard.png)

Tindakan ini secara otomatis membuat class baru, BigCard, di akhir file saat ini. Class tersebut akan terlihat seperti berikut:
![Hasil Menambahkan Widget](/images/classbigcard.png)

#### Menambahkan Card
Sekarang saatnya membuat widget baru ini menjadi UI tebal yang kita bayangkan di awal bagian ini.

Temukan class BigCard dan metode build() yang berada di dalamnya. Sama seperti sebelumnya, panggil menu Refactor pada widget Text. Namun, kali ini Anda tidak akan mengekstrak widget.

Sebagai gantinya, pilih Wrap with Padding. Tindakan ini menciptakan widget induk baru di sekitar widget Text bernama Padding. Setelah menyimpannya, Anda akan melihat bahwa kata acak tersebut telah memiliki ruang yang lebih luas.
![Hasil Padding](/images/padding.png)
Kode ini menggabungkan widget Padding, dan juga Text, dengan widget Card.<br>
![Hasil Tambah Padding](/images/hasil-padding.png)

#### Tema dan Gaya
Untuk membuat kartu menjadi lebih menarik, beri warna yang lebih kaya pada kartu tersebut. Karena ada baiknya untuk menjaga skema warna yang konsisten, gunakan Theme aplikasi untuk memilih warna.

Buat perubahan berikut untuk metode build() BigCard.
![Hasil Tema dan Gaya](/images/tema-gaya.png)

Kedua baris baru ini melakukan banyak hal:

Pertama, kode ini meminta tema aplikasi saat ini dengan Theme.of(context).
Kemudian, kode ini menentukan warna kartu agar sama dengan properti colorScheme dari tema. Skema warna menampung banyak warna, dan primary adalah warna aplikasi yang paling terlihat dan mencolok.
Kini, kartu telah diwarnai dengan warna primer aplikasi:
![Hasil Tambah Tema dan Gaya](/images/hasil-temagaya.png)

#### TextTheme
Kartu tersebut masih memiliki masalah: ukuran teks terlalu kecil dan warnanya membuat teks sulit dibaca. Untuk memperbaiki masalah ini, buat perubahan berikut pada metode build() BigCard.
![Hasil TextTheme](/images/texttheme.png)
Kini, aplikasi akan terlihat seperti berikut:
![Hasil Tambah TextTheme](/images/hasil-texttheme.png)

Gunakan properti semanticsLabel Text untuk mengganti konten visual widget teks dengan konten semantik yang lebih sesuai untuk pembaca layar:
![Hasil modif Text](/images/modif-text.png)

#### Menempatkan UI di tengah
Pertama, ingatlah bahwa BigCard adalah bagian dari Column. Secara default, kolom menggabungkan turunan kolom di bagian atas, tetapi kita dapat mengganti ini dengan mudah. Buka metode build() MyHomePage, dan buat perubahan berikut:
![Hasil modif tampilan](/images/center.png)

Tindakan ini menempatkan turunan dalam Column di tengah pada sumbu utamanya (vertikal).
![Hasil center tampilan](/images/hasil-center.png)

Anda dapat menempatkan kolom itu sendiri di tengah. Letakkan kursor Anda di Column, buka menu Refactor (dengan Ctrl+. atau Cmd+.), lalu pilih Wrap with Center.
(![Hasil Wrap](/images/wrap.png))

Kini, aplikasi akan terlihat seperti berikut:
![Hasil Tampilan Wrap](/images/hasil-wrap.png)

Jika mau, Anda dapat menyesuaikan tampilan ini lebih lanjut.

- Anda dapat menghapus widget Text di atas BigCard. Dapat dipastikan bahwa teks deskriptif ("Ide LUAR BIASA acak:") tidak lagi diperlukan karena UI tersebut sudah jelas meskipun tanpa teks deskriptif. Selain itu, dengan begitu UI terlihat lebih bersih.
- Anda juga dapat menambahkan widget SizedBox(height: 10) di antara BigCard dan ElevatedButton. Dengan begitu, ada sedikit pemisah di antara kedua widget tersebut. Widget SizedBox hanya mengambil ruang dan tidak merender apa pun dengan sendirinya. Widget ini biasa digunakan untuk membuat "jarak" visual.<br>

Dengan perubahan opsional, MyHomePage mencakup kode berikut:
![Hasil Modifikasi](/images/modifikasi.png)

Aplikasinya akan terlihat seperti berikut:
![Hasil Modifikasi Tampilan](/images/hasil-modifikasi.png)

### Menambahkan Fungsi
#### Menambahkan Logika Bisnis
![Hasil Logika Bisnis](/images/logika-bisnis.png)

#### Menambahkan Button
![Hasil Wrap Row](/images/wrap-row.png)

![Hasil Modifikasi Home Page](/images/modif-homepage.png)

Hasilnya UI kembali ke tempat sebelumnya.
![Hasil Home Page](/images/hasil-homepage.png)

Berikutnya, tambahkan button Like dan hubungkan ke toggleFavorite().
![Hasil Button Like](/images/button-like.png)

Aplikasi akan terlihat seperti berikut:
![Hasil Tampilan Button Like 1](/images/hasil-button-like1.png)
![Hasil Tampilan Button Like 1](/images/hasil-button-like2.png)


### Menambahkan kolom samping navigasi
Untuk mencapai inti dari langkah ini secepat mungkin, pisahkan MyHomePage menjadi 2 widget terpisah.
![Hasil Langkah 1](/images/langkah-1.png)

Saat disimpan, Anda akan melihat sisi visual UI telah siap—tetapi tidak bekerja. Mengklik ♥︎ (hati) pada kolom samping navigasi tidak melakukan apa pun.
![Hasil Tampilan Langkah 1](/images/tampilan-langkah-1.png)

#### Widget stateless versus stateful
![Proses Langkah 1](/images/proses-2.png)

![Hasil Langkah 2](/images/langkah-2.png)

#### setState
Widget stateful baru hanya perlu melacak satu variabel: selectedIndex. Buat 3 perubahan berikut untuk _MyHomePageState:
![Hasil Langkah 3](/images/langkah-3.png)

Hasil Tampilan:
![Hasil Tampilan Langkah 3](/images/tampilan-langkah-3.png)

#### Menggunakan selectedIndex
Tempatkan kode berikut di bagian atas metode build _MyHomePageState, tepat sebelum return Scaffold:
![Hasil Langkah 4](/images/langkah-4.png)

Aplikasi sekarang beralih di antara GeneratorPage kita dan placeholder yang akan segera menjadi halaman Favorites.
![Hasil Tampilan Langkah 4](/images/tampilan-langkah-4.png)

#### Tingkat respons
Dalam hal ini, widget yang digunakan adalah LayoutBuilder. Widget ini memungkinkan Anda mengubah pohon widget tergantung pada seberapa banyak ruang yang tersedia yang dimiliki.

Sekali lagi, gunakan menu Refactor Flutter di VS Code untuk membuat perubahan yang diperlukan. Namun, proses kali ini sedikit lebih rumit:

1. Dalam metode build _MyHomePageState, letakkan kursor Anda pada Scaffold.
2. Buka menu Refactor dengan Ctrl+. (Windows/Linux) atau Cmd+. (Mac).
3. Pilih Wrap with Builder dan tekan Enter.
4. Modifikasi nama Builder yang baru ditambahkan menjadi LayoutBuilder.
5. Modifikasi daftar parameter callback dari (context) menjadi (context, constraints).
![Hasil Wrap Builder](/images/wrap-builder.png)

Sekarang kode Anda dapat memutuskan untuk menampilkan label dengan membuat kueri constraints saat ini atau tidak. Buat perubahan baris tunggal berikut untuk metode build _MyHomePageState:
![Hasil Langkah 5](/images/langkah-5.png)

Sekarang aplikasi Anda merespons lingkungannya, seperti ukuran layar, orientasi, dan platform. Dengan kata lain, aplikasi Anda sudah responsif.
![Hasil Tampilan Langkah 5](/images/tampilan-langkah-5.png)

### Menambahkan halaman baru
Berikut ini merupakan salah satu cara untuk menerapkan halaman favorit, yaitu menampilkan daftar favorites dalam widget stateless baru, FavoritesPage, lalu menampilkan widget tersebut, bukan Placeholder.<br>
Berikut class FavoritesPage baru:
![Hasil Tambah Halaman Baru](/images/tambah-halaman.png)

Hasil Tampilan:
![Hasil Tambah Halaman Baru](/images/hasil-namer_app.gif)