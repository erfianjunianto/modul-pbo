# MODUL MATA KULIAH PEMROGRAMAN BERBASIS OBJEK

**(SI-301 | 3 SKS)**

---

**Program Studi:** Sistem Informasi
**Semester:** 3
**Bahasa Pemrograman:** PHP
**Dosen Pengampu:** [Erfian Junianto]

---

## Deskripsi Mata Kuliah

Mata kuliah ini memberikan pemahaman fundamental mengenai paradigma Pemrograman Berbasis Objek (PBO/OOP). Mahasiswa akan beralih dari cara berpikir prosedural menjadi berpikir dalam kerangka objek, properti, dan metode. Fokus utama adalah menguasai empat pilar PBO (Encapsulation, Inheritance, Polymorphism, Abstraction) serta fitur-fitur modern PHP seperti `traits`, `namespaces`, dan `autoloading`.

## Capaian Pembelajaran Lulusan (CPL)

Setelah menyelesaikan mata kuliah ini, mahasiswa diharapkan **mampu merancang dan mengimplementasikan aplikasi skala kecil menggunakan prinsip-prinsip PBO secara tepat, bersih, dan terstruktur.**

---

## MODUL 1: FONDASI PBO

### Pertemuan 1: Pengenalan Paradigma & Kontrak Kuliah

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu membedakan paradigma pemrograman prosedural dengan PBO dan memahami konsep dasar `Class` dan `Object`.
* **Materi Pembelajaran:**
  1. **Kontrak Kuliah:** Penjelasan RPS, sistem penilaian (Tugas, UTS, UAS), dan etika kelas.
  2. **Paradigma Prosedural:**
     * Fokus pada *urutan langkah* atau *prosedur*.
     * Data (`variabel`) dan logika (`fungsi`) seringkali terpisah.
     * Contoh: Anda membuat serangkaian fungsi `hitungLuas()`, `hitungKeliling()`, yang beroperasi pada variabel global `$panjang`, `$lebar`.
  3. **Paradigma Berbasis Objek (PBO):**
     * Fokus pada *objek* dari dunia nyata.
     * Menggabungkan data (disebut **Property**) dan logika (disebut **Method**) ke dalam satu kesatuan yang disebut **Class**.
  4. **Analogi Kunci:**
     * **Class:** Sebuah *blueprint* atau cetakan. Contoh: `Blueprint Mobil`.
     * **Object (Instance):** Hasil nyata dari *blueprint* tersebut. Contoh: `Mobil Avanza Budi` atau `Mobil Brio Sari`.
  5. **Istilah Dasar:**
     * **Class:** Template untuk membuat objek (`Mobil`).
     * **Object:** Instansiasi/wujud nyata dari sebuah class (`$mobilSaya`).
     * **Property (Atribut):** Data yang dimiliki oleh class (`$warna`, `$merk`, `$jumlahRoda`).
     * **Method (Behavior):** Hal yang bisa dilakukan oleh class (`maju()`, `mundur()`, `isiBensin()`).

---

### Pertemuan 2: Sintaks Dasar: Class, Object, Property, Method

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menulis sintaks PHP untuk membuat `class`, meng-instansiasi `object`, mendefinisikan `property`, dan memanggil `method`.
* **Materi Pembelajaran:**
  1. **Sintaks `class`:** Menggunakan keyword `class`.
  2. **Sintaks `new`:** Keyword untuk membuat objek (instansiasi) dari sebuah class.
  3. **Mendefinisikan Property:** Variabel di dalam class (dulu pakai `var`, sekarang disarankan pakai `public`, `private`, atau `protected`).
  4. **Mendefinisikan Method:** Fungsi di dalam class.
  5. **Keyword `$this`:** Ini adalah *kata kunci ajaib* yang merujuk pada "objek ini" atau "diri sendiri". `$this` digunakan di dalam method untuk mengakses property milik objek tersebut.
* **Contoh Kode (PHP):**
  ```php
  <?php
  // 1. Mendefinisikan Class (Blueprint)
  class Mobil {
      // 2. Property (Data)
      public $warna = "Merah";
      public $merk = "Toyota";

      // 3. Method (Behavior/Fungsi)
      public function maju() {
          // 4. Menggunakan $this untuk mengakses property milik objek ini
          return "Mobil " . $this->merk . " sedang maju!";
      }

      public function klakson() {
          return "Tiiin!";
      }
  }

  // 5. Instansiasi Object (Membuat mobil nyata dari blueprint)
  $mobilSaya = new Mobil();
  $mobilTetangga = new Mobil();

  // 6. Mengakses Property
  echo $mobilSaya->warna; // Output: Merah

  // Kita bisa ubah property-nya
  $mobilTetangga->merk = "Honda";

  // 7. Memanggil Method
  echo $mobilSaya->maju(); // Output: Mobil Toyota sedang maju!
  echo $mobilTetangga->maju(); // Output: Mobil Honda sedang maju!
  ?>
  ```
* **Tugas Mandiri 1:**
  Buatlah `class` `Mahasiswa` dengan property `public $nim`, `public $nama`, dan `public $ipk`. Buat method `public function belajar()` (mengembalikan string "Saya sedang belajar...") dan `public function tampilkanInfo()` (mengembalikan string "Nama: [nama], NIM: [nim]"). Buat 2 objek mahasiswa (`$mhs1`, `$mhs2`) dari class tersebut dan panggil method `tampilkanInfo()`-nya.

---

### Pertemuan 3: Constructor & Visibility (Access Modifier)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menggunakan `constructor` untuk inisialisasi objek dan memahami perbedaan `public` vs `private`.
* **Materi Pembelajaran:**
  1. **Masalah:** Bagaimana jika kita ingin `$mobilSaya` warnanya `Biru` dan `$mobilTetangga` warnanya `Hitam` *saat pertama kali dibuat*, tanpa harus di-set manual satu per satu?
  2. **`__construct()` (Constructor):** Ini adalah *magic method* yang otomatis dipanggil **satu kali** saat objek dibuat (saat keyword `new` digunakan). Tujuannya adalah untuk inisialisasi nilai awal property.
  3. **Visibility (Access Modifier):** Aturan hak akses.
     * `public`: Bisa diakses dari *mana saja* (dari luar class maupun di dalam class).
     * `private`: **Hanya** bisa diakses dari *dalam class* itu sendiri. Tidak bisa diakses dari luar.
     * `protected`: (Akan dibahas di modul Inheritance).
* **Contoh Kode (PHP):**
  ```php
  <?php
  class Mahasiswa {
      public $nama;     // Bisa diakses dari luar
      private $nim;    // Hanya bisa diakses di dalam class ini

      // 3. Constructor: dipanggil saat 'new Mahasiswa(...)'
      public function __construct($namaAwal, $nimAwal) {
          $this->nama = $namaAwal;
          $this->nim = $nimAwal;
          echo "Objek Mahasiswa " . $this->nama . " telah dibuat! <br>";
      }

      // Method public untuk mengakses $nim yang private
      public function tampilkanInfo() {
          // $nim bisa diakses di sini karena masih di dalam class
          echo "Nama: " . $this->nama . ", NIM: " . $this->nim . "<br>";
      }
  }

  // Saat 'new', kita WAJIB menyertakan parameter untuk constructor
  $mhs1 = new Mahasiswa("Budi", "12345");
  $mhs2 = new Mahasiswa("Sari", "67890");

  // Mengakses property public (SUKSES)
  echo $mhs1->nama; // Output: Budi

  // Mengakses property private (ERROR!)
  // echo $mhs1->nim; // Ini akan menghasilkan Fatal Error!

  // Cara yang benar mengakses info NIM adalah lewat method public
  $mhs1->tampilkanInfo(); // Output: Nama: Budi, NIM: 12345
  $mhs2->tampilkanInfo(); // Output: Nama: Sari, NIM: 67890
  ?>
  ```

---

### Pertemuan 4: Prinsip Encapsulation (Getter & Setter)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menerapkan prinsip *Encapsulation* (pembungkusan) menggunakan method `getter` dan `setter` untuk validasi data.
* **Materi Pembelajaran:**
  1. **Encapsulation (Pilar 1 PBO):** Konsep "membungkus" data. Caranya adalah dengan membuat property `private` dan menyediakan "pintu" khusus berupa method `public` untuk mengaksesnya.
  2. **Kenapa Repot?** Untuk **Validasi** dan **Kontrol**.
     * Contoh: Kita tidak mau ada yang meng-set `$ipk` menjadi 5.0 atau -1.0.
     * Contoh: Kita tidak mau ada yang meng-set `$nim` dengan huruf.
  3. **Getter:** Method `public` untuk *mendapatkan* (get) nilai property `private`. (Konvensi: diawali `get...()`).
  4. **Setter:** Method `public` untuk *mengatur* (set) nilai property `private`, di sinilah tempat validasinya. (Konvensi: diawali `set...()`).
* **Contoh Kode (PHP):**
  ```php
  <?php
  class Mahasiswa {
      public $nama;
      private $ipk; // Dibungkus!

      public function __construct($namaAwal) {
          $this->nama = $namaAwal;
      }

      // 4. Setter: Pintu masuk untuk MENGATUR $ipk
      public function setIpk($nilai) {
          // 2. Ada validasi di sini!
          if ($nilai >= 0.0 && $nilai <= 4.0) {
              $this->ipk = $nilai;
          } else {
              echo "Error: IPK tidak valid! <br>";
          }
      }

      // 3. Getter: Pintu keluar untuk MENDAPATKAN $ipk
      public function getIpk() {
          if (isset($this->ipk)) {
              return $this->ipk;
          } else {
              return "IPK belum di-set";
          }
      }
  }

  $mhs2 = new Mahasiswa("Sari");

  // Kita tidak bisa: $mhs2->ipk = 5.0; (Error karena private)

  // Kita HARUS lewat Setter:
  $mhs2->setIpk(3.75); // Sukses
  $mhs2->setIpk(5.0);  // Output: Error: IPK tidak valid!

  // Kita HARUS lewat Getter:
  echo "IPK " . $mhs2->nama . " adalah " . $mhs2->getIpk();
  // Output: IPK Sari adalah 3.75
  ?>
  ```
* **Tugas Mandiri 2:**
  Modifikasi `class` `Mahasiswa` dari Tugas 1.
  1. Ubah `nim` dan `ipk` menjadi `private`. `nama` tetap `public`.
  2. Buat `constructor` yang menerima `nim` dan `nama`.
  3. Buat method `public function setIpk($nilai)` (dengan validasi 0-4).
  4. Buat method `public function getIpk()` dan `public function getNim()`.
  5. Ubah method `tampilkanInfo()` agar menggunakan getter.

---

## MODUL 2: PILAR PBO (INHERITANCE & POLYMORPHISM)

### Pertemuan 5: Inheritance (Pewarisan)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menerapkan prinsip *Inheritance* (pilar 2 PBO) untuk *code reusability* menggunakan keyword `extends` dan `protected`.
* **Materi Pembelajaran:**
  1. **Konsep "Is-A" (Adalah):** Inheritance adalah hubungan "adalah".
     * `Manager` **adalah** seorang `Karyawan`.
     * `Laptop` **adalah** sebuah `Produk`.
  2. **Tujuan:** *Code Reusability* (Penggunaan Ulang Kode). Kita tidak perlu copy-paste `property` dan `method` yang sama (`nama`, `gaji`, `absensi()`) di class `Manager`, `Supervisor`, `Staff`, dll.
  3. **Sintaks:** Menggunakan keyword `extends`.
  4. **Istilah:**
     * `Parent Class` (Superclass): Class yang mewariskan (`Karyawan`).
     * `Child Class` (Subclass): Class yang mewarisi (`Manager`).
  5. **Revisi Visibility:** `protected`
     * `protected`: Seperti `private` (tidak bisa diakses dari luar), **TAPI** boleh diakses oleh `child class`-nya. Ini sangat penting untuk inheritance.
  6. **Memanggil Induk:** `parent::__construct()` untuk memanggil constructor milik parent.
* **Contoh Kode (PHP):**
  ```php
  <?php
  // 4. Parent Class (Superclass)
  class Karyawan {
      public $nama;
      protected $gaji; // protected agar bisa diakses child class

      public function __construct($nama, $gaji) {
          $this->nama = $nama;
          $this->gaji = $gaji;
      }

      public function getInfo() {
          return "Nama: " . $this->nama . ", Gaji: Rp " . $this->gaji;
      }
  }

  // 5. Child Class (Subclass)
  class Manager extends Karyawan {
      // Punya semua property & method Karyawan (nama, gaji, getInfo)

      // Ditambah property khusus Manager
      public $tunjangan;

      public function __construct($nama, $gaji, $tunjangan) {
          // 6. Panggil constructor parent
          parent::__construct($nama, $gaji); 
          $this->tunjangan = $tunjangan;
      }

      // Method khusus Manager
      public function getInfoLengkap() {
          // Kita bisa akses $this->gaji (karena protected)
          return "Nama: " . $this->nama . 
                 ", Gaji: Rp " . $this->gaji . 
                 ", Tunjangan: Rp " . $this->tunjangan;
      }
  }

  $staff = new Karyawan("Andi", 4000000);
  $manager = new Manager("Budi", 8000000, 2000000);

  echo $staff->getInfo(); // Output: Nama: Andi, Gaji: Rp 4000000

  // Objek Manager punya method dari parent DAN method-nya sendiri
  echo $manager->getInfo(); // Output: Nama: Budi, Gaji: Rp 8000000
  echo $manager->getInfoLengkap(); // Output: Nama: Budi, Gaji: Rp 8000000, Tunjangan: Rp 2000000
  ?>
  ```
* **Tugas Mandiri 3:**
  Buat `class` `Produk` (Parent) dengan `protected $merek` dan `protected $harga`. Buat `constructor`-nya. Lalu buat `class` `Laptop` (Child) yang `extends` `Produk`. `Laptop` punya property tambahan `public $ukuranLayar`. Buat `constructor` di `Laptop` yang juga memanggil `constructor` `parent`.

---

### Pertemuan 6: Method Overriding & Keyword `final`

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu meng-override (menimpa) method parent di child class dan memahami kegunaan keyword `final`.
* **Materi Pembelajaran:**
  1. **Overriding:** Mendefinisikan ulang *method* yang sama (nama sama, parameter sama) di `child class`. Tujuannya agar `child class` punya implementasi yang lebih spesifik.
  2. **Contoh:** Method `getInfo()` di `Karyawan` mungkin berbeda dengan `getInfo()` di `Manager`. `Manager` mungkin ingin langsung menampilkan tunjangannya juga.
  3. **Keyword `final` (pada Method):** Melarang `child class` untuk meng-override method tersebut.
  4. **Keyword `final` (pada Class):** Melarang sebuah `class` untuk di-`extends` (diwarisi).
* **Contoh Kode (PHP):**
  ```php
  <?php
  class Karyawan {
      // ... (constructor sama seperti di atas) ...

      // 1. Method ini akan kita override di child
      public function getInfo() {
          return "Nama: " . $this->nama . ", Gaji: Rp " . $this->gaji;
      }

      // 3. Method ini TIDAK BOLEH di-override
      final public function getAbsensi() {
          return "Mencatat absensi harian untuk " . $this->nama;
      }
  }

  class Manager extends Karyawan {
      // ... (constructor sama seperti di atas) ...

      // 2. Overriding method getInfo()
      public function getInfo() {
          // Kita bisa panggil method asli parent, lalu tambahkan info
          $infoParent = parent::getInfo(); 
          return $infoParent . ", Tunjangan: Rp " . $this->tunjangan;
      }

      /*
      // 4. Jika kita coba uncomment kode ini, akan ERROR!
      public function getAbsensi() {
          return "Absensi khusus manager";
      }
      */
  }

  // 3. Class ini tidak bisa di-extends
  final class CEO extends Karyawan {
      // ...
  }

  $manager = new Manager("Budi", 8000000, 2000000);
  // PHP akan memanggil getInfo() versi Manager, bukan versi Karyawan
  echo $manager->getInfo(); 
  // Output: Nama: Budi, Gaji: Rp 8000000, Tunjangan: Rp 2000000
  ?>
  ```

---

### Pertemuan 7: Polymorphism (Bentuk Banyak)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menerapkan prinsip *Polymorphism* (pilar 3 PBO) untuk menciptakan kode yang fleksibel.
* **Materi Pembelajaran:**
  1. **Polymorphism (Banyak Bentuk):** Ini adalah konsep *powerful* di mana sebuah objek `child` (misal: `Manager`) bisa diperlakukan sebagai objek `parent` (misal: `Karyawan`).
  2. **Manfaat:** Kode kita jadi super fleksibel. Kita bisa membuat fungsi yang menerima `Karyawan` sebagai parameter. Saat kita panggil fungsi itu, kita bisa masukkan objek `Karyawan` biasa, `Manager`, `Supervisor`, `Intern`, dll (asalkan mereka semua `extends Karyawan`).
  3. Fungsi tersebut akan secara "pintar" memanggil method `getInfo()` yang *sesuai* dengan objek aslinya (jika objeknya `Manager`, ia panggil `getInfo()` milik `Manager`).
* **Contoh Kode (PHP):**
  ```php
  <?php
  // (Menggunakan class Karyawan dan Manager dari atas)

  class Supervisor extends Karyawan {
      // Override getInfo() versi Supervisor
      public function getInfo() {
          return "[SUPERVISOR] Nama: " . $this->nama . ", Gaji: Rp " . $this->gaji;
      }
  }

  // --- INI KEAJAIBAN POLYMORPHISM ---
  // 2. Fungsi ini hanya tahu Karyawan, dia tidak peduli
  // apakah itu Manager, Supervisor, atau Karyawan biasa.
  // Tipe data parameter adalah 'Karyawan' (parent class)
  function cetakInfoKaryawan(Karyawan $karyawan) {
      // 3. PHP otomatis memanggil method getInfo()
      // yang BENAR sesuai objek aslinya.
      echo $karyawan->getInfo() . "<br>";
  }

  // Buat 3 objek berbeda, tapi 1 tipe (Karyawan)
  $staff = new Karyawan("Andi", 4000000);
  $manager = new Manager("Budi", 8000000, 2000000);
  $supervisor = new Supervisor("Citra", 6000000);

  // Kita panggil fungsi yang sama dengan 3 TIPE OBJEK BERBEDA
  cetakInfoKaryawan($staff); 
  // Output: Nama: Andi, Gaji: Rp 4000000

  cetakInfoKaryawan($manager); 
  // Output: Nama: Budi, Gaji: Rp 8000000, Tunjangan: Rp 2000000

  cetakInfoKaryawan($supervisor); 
  // Output: [SUPERVISOR] Nama: Citra, Gaji: Rp 6000000
  ?>
  ```
* **Tugas Mandiri 4:**
  Buat `class` `Hewan` dengan method `bersuara()`. Buat 2 `child class`: `Kucing` dan `Anjing` (keduanya `extends` `Hewan`). Override method `bersuara()` di `Kucing` (return "Meow!") dan `Anjing` (return "Guk Guk!"). Buat fungsi `dengarSuara(Hewan $hewan)` yang memanggil `$hewan->bersuara()`. Panggil fungsi `dengarSuara()` dengan objek `Kucing` dan `Anjing`.

---

### Pertemuan 8: UJIAN TENGAH SEMESTER (UTS)

* **Bentuk:** Ujian Praktik/Studi Kasus Kecil.
* **Cakupan Materi:** Pertemuan 1 s.d. 7.
* **Fokus:** Mahasiswa diminta membuat beberapa `class` yang saling berhubungan (misal: Sistem rental mobil, sistem perpustakaan sederhana) yang menerapkan:
  1. Class, Object, Constructor.
  2. Encapsulation (Getter & Setter).
  3. Inheritance (`extends`).
  4. Polymorphism (Overriding & fungsi dengan tipe parent).

---

## MODUL 3: ABSTRAKSI & KONTRAK

### Pertemuan 9: Abstract Class & Abstract Method

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menerapkan prinsip *Abstraction* (pilar 4 PBO) menggunakan `abstract class` untuk membuat "template" class.
* **Materi Pembelajaran:**
  1. **Abstraksi:** Menyembunyikan detail implementasi dan hanya menunjukkan fungsionalitas esensial.
  2. **`abstract class`:** Sebuah `class` "template" atau "konsep" yang **tidak bisa di-instansiasi** (tidak bisa di-`new`). Tujuannya murni untuk di-`extends` oleh `child class`.
  3. **`abstract method`:** Sebuah method di dalam `abstract class` yang *tidak punya isi* (tidak punya *body* `{}`). Ini adalah sebuah "kontrak paksa".
  4. **Aturan Emas (Kontrak):** Jika sebuah `class` `extends` sebuah `abstract class` yang punya `abstract method`, maka `class` tersebut **WAJIB** meng-implementasikan (meng-override) semua `abstract method` tersebut.
* **Contoh Kode (PHP):**
  ```php
  <?php
  // 2. Ini adalah class template, tidak bisa di-new
  abstract class Bentuk {
      protected $nama;

      public function __construct($nama) {
          $this->nama = $nama;
      }

      // 3. Abstract method (Kontrak): tidak punya isi
      // "Hei child class, kamu WAJIB punya method hitungLuas!"
      abstract public function hitungLuas();

      // Abstract class Boleh punya method biasa
      public function getNama() {
          return $this->nama;
      }
  }

  class Persegi extends Bentuk {
      private $sisi;

      public function __construct($sisi) {
          parent::__construct("Persegi");
          $this->sisi = $sisi;
      }

      // 4. Implementasi kontrak dari parent
      public function hitungLuas() {
          return $this->sisi * $this->sisi;
      }
  }

  class Lingkaran extends Bentuk {
      private $radius;

      public function __construct($radius) {
          parent::__construct("Lingkaran");
          $this->radius = $radius;
      }

      // 4. Implementasi kontrak dari parent
      public function hitungLuas() {
          return 3.14 * $this->radius * $this->radius;
      }
  }

  $persegi = new Persegi(10);
  echo $persegi->getNama() . ": " . $persegi->hitungLuas(); // Output: Persegi: 100

  // $bentuk = new Bentuk("Bentuk"); // Ini akan ERROR!
  ?>
  ```
* **Tugas Mandiri 5:**
  Buat `abstract class` `Senjata` dengan `abstract method` `serang()`. Buat 2 `child class`: `Pedang` dan `Pistol` yang `extends` `Senjata`. Implementasikan method `serang()` di kedua `child class` (misal: "Pedang menebas!", "Pistol menembak!").

---

### Pertemuan 10: Interface (Antarmuka)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menggunakan `interface` untuk mendefinisikan "kemampuan" (kontrak murni) yang bisa di-implementasi oleh banyak class.
* **Materi Pembelajaran:**
  1. **Masalah:** PHP adalah *Single Inheritance*. Sebuah `class` hanya bisa `extends` **satu** `parent class`. Lalu bagaimana jika `Bebek` ingin mewarisi sifat dari `Hewan` (bisa makan) dan `BendaTerbang` (bisa terbang)?
  2. **Solusi: `interface`**. Sebuah `interface` adalah "kontrak" 100% murni.
  3. **Aturan Interface:**
     * Isinya *hanya* deklarasi `method` (semua otomatis `public` dan `abstract`).
     * Tidak boleh punya `property`.
     * Keyword untuk menggunakannya: `implements` (bukan `extends`).
     * Sebuah `class` boleh `implements` **lebih dari satu** `interface`.
  4. **Analogi:** `Interface` adalah "Kemampuan" (Can-Do).
     * `class` `Burung` dan `class` `Pesawat` bisa `implements` `BisaTerbang`.
     * `class` `Smartphone` dan `class` `Laptop` bisa `implements` `BisaTerhubungWifi`.
* **Contoh Kode (PHP):**
  ```php
  <?php
  // Interface adalah "kontrak kemampuan"
  interface BisaTerbang {
      public function terbang();
  }

  interface BisaBerenang {
      public function berenang();
  }

  class Burung implements BisaTerbang {
      public function terbang() {
          echo "Burung terbang tinggi di angkasa. <br>";
      }
  }

  class Ikan implements BisaBerenang {
      public function berenang() {
          echo "Ikan berenang di dalam air. <br>";
      }
  }

  // Class ini super! Bisa implementasi BANYAK kemampuan
  // Dia 'extends' 1 parent, dan 'implements' banyak interface
  class Bebek implements BisaTerbang, BisaBerenang {
      public function terbang() {
          echo "Bebek terbang, tapi tidak terlalu tinggi. <br>";
      }

      public function berenang() {
          echo "Bebek berenang di permukaan danau. <br>";
      }
  }

  $burung = new Burung();
  $bebek = new Bebek();
  $burung->terbang();
  $bebek->terbang();
  $bebek->berenang();
  ?>
  ```
* **Tugas Mandiri 6:**
  Buat `interface` `BisaDiunduh` dengan method `download()`. Buat `class` `Lagu` dan `class` `Ebook` yang `implements` `BisaDiunduh`. Implementasikan method `download()` yang sesuai untuk keduanya.

---

### Pertemuan 11: Kapan Pakai Abstract Class vs Interface?

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu mengambil keputusan desain untuk menggunakan `abstract class` atau `interface` berdasarkan studi kasus.
* **Materi Pembelajaran:** Ini adalah sesi diskusi dan pengambilan keputusan desain.
  1. **Gunakan `Abstract Class` (Hubungan "Is-A"):**
     * Saat Anda ingin **berbagi kode** (method non-abstract) dan **property** di antara beberapa `child class` yang *mirip*.
     * Hubungan: "Is-A" (adalah sebuah).
     * Contoh: `Persegi` **adalah** `Bentuk`. `Lingkaran` **adalah** `Bentuk`. Keduanya berbagi `property` `$nama` dan kewajiban `hitungLuas()`.
  2. **Gunakan `Interface` (Hubungan "Can-Do"):**
     * Saat Anda ingin mendefinisikan **kemampuan** (capability) yang bisa dimiliki oleh `class` yang *sangat berbeda-beda*.
     * Anda tidak berbagi kode, hanya "menandai" bahwa class itu bisa melakukan sesuatu.
     * Hubungan: "Can-Do" (bisa melakukan).
     * Contoh: `Bebek` **bisa** `Terbang`. `Pesawat` **bisa** `Terbang`. Keduanya sangat berbeda, tapi punya 1 kemampuan yang sama.
  3. **Studi Kasus Diskusi:** Sistem E-commerce.
     * `Produk`: Sebaiknya `abstract class`. Kenapa? Karena semua produk (`Laptop`, `Baju`, `Buku`) punya property yang sama (`nama`, `harga`, `sku`) dan method yang sama (`getInfo()`).
     * `BisaDikirim`: Sebaiknya `interface`. Kenapa? Karena `Laptop` dan `Baju` `implements` `BisaDikirim`. Tapi `ProdukDigital` (seperti Ebook) tidak. Ini adalah "kemampuan" tambahan.
     * `BisaDiskon`: Sebaiknya `interface`. Semua `Produk` bisa `implements` `BisaDiskon`.

---

## MODUL 4: FITUR LANJUTAN & STUDI KASUS

### Pertemuan 12: `static` Property, `static` Method & `Traits`

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu menggunakan `static` property/method untuk *utility* dan `traits` untuk *code reuse* horizontal.
* **Materi Pembelajaran:**
  1. **`static` Property/Method:**
     * Property/method yang "menempel" di `class`-nya, bukan di `object`-nya.
     * **Tidak perlu** `new` untuk memanggilnya.
     * **Tidak bisa** menggunakan `$this`. Sebagai gantinya, gunakan `self::`.
     * Biasanya dipakai untuk fungsi *utility* (Helper) atau *counter*.
  2. **`Traits`:**
     * Solusi PHP untuk *multiple inheritance*.
     * Analogi: "Menyuntikkan" atau "Copy-paste" satu set method ke dalam `class` manapun.
     * Sintaks: `trait NamaTrait { ... }` dan `class NamaClass { use NamaTrait; }`.
* **Contoh Kode (PHP):**
  ```php
  <?php
  // 1. Contoh Static
  class Kalkulator {
      public static $totalOperasi = 0; // Menempel di class

      // Static method, dipanggil pakai ::
      public static function tambah($a, $b) {
          self::$totalOperasi++; // Akses static property pakai self::
          return $a + $b;
      }
  }

  // Panggil static method tanpa membuat objek
  echo "Hasil: " . Kalkulator::tambah(10, 5) . "<br>"; // Output: Hasil: 15
  echo "Total Operasi: " . Kalkulator::$totalOperasi . "<br>"; // Output: Total Operasi: 1

  // 2. Contoh Trait
  trait BisaLog {
      // Ini adalah sekumpulan method
      public function log($pesan) {
          echo "[LOG PENTING]: " . $pesan . "<br>";
      }
  }

  class Pengguna {
      use BisaLog; // "Suntikkan" kemampuan log

      public function daftar() {
          // ... logika mendaftar ...
          $this->log("Pengguna baru mendaftar.");
      }
  }

  class Database {
      use BisaLog; // Trait bisa dipakai di banyak class

      public function koneksiGagal() {
          // ...
          $this->log("Koneksi database GAGAL!");
      }
  }

  $userBaru = new Pengguna();
  $userBaru->daftar(); // Output: [LOG PENTING]: Pengguna baru mendaftar.
  ?>
  ```
* **Tugas Mandiri 7:**
  Buat `class` `Helper` yang memiliki `static method` `formatRupiah($angka)` yang mengembalikan string (misal: "Rp 10.000"). Panggil method tersebut tanpa membuat objek `Helper`.

---

### Pertemuan 13: Namespaces & Autoloading (PSR-4)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu mengorganisir kode menggunakan `namespaces` dan `autoloading` (Composer/PSR-4). Ini adalah **standar industri**.
* **Materi Pembelajaran:**
  1. **Masalah 1:** Apa jadinya jika ada 2 `class` dengan nama sama di proyek besar? (Misal: `Toko\Produk` dan `Perpustakaan\Produk`). Kode akan *crash*.
  2. **Solusi 1: `Namespaces`**. Memberi "alamat" atau "folder virtual" untuk `class` kita.
     * `namespace App\Models;` (di baris paling atas file `Produk.php`).
  3. **Masalah 2:** Capek menulis `require_once 'file.php';` untuk puluhan file.
  4. **Solusi 2: Autoloading**. Mekanisme otomatis me-`require` file saat `class`-nya dipanggil.
  5. **Standard Industri: Composer & PSR-4**. Kita tidak akan buat autoloader manual. Kita akan pakai **Composer** (manajer paket PHP).
* **Contoh (Struktur File & Kode):**
  ```
  /proyek-pbo
      /src
          /Models         <-- Namespace App\Models
              Produk.php
              User.php
          /Services       <-- Namespace App\Services
              Keranjang.php
      composer.json
      index.php
      /vendor         <-- Dibuat otomatis oleh Composer
  ```

  * **File: `composer.json`** (Konfigurasi autoloader)

    ```json
    {
        "autoload": {
            "psr-4": {
                "App\\": "src/"
            }
        }
    }
    ```

    (Jalankan `composer dump-autoload` di terminal)
  * **File: `src/Models/Produk.php`**

    ```php
    <?php
    namespace App\Models; // 2. Tentukan "alamat"

    class Produk {
        public $nama;
    }
    ?>
    ```
  * **File: `index.php`** (File utama)

    ```php
    <?php
    // 4. Cukup panggil autoloader 1x
    require_once 'vendor/autoload.php'; 

    // 5. 'Import' class yang ingin dipakai
    use App\Models\Produk;

    // 6. Langsung 'new' tanpa 'require_once'
    $produk1 = new Produk();
    $produk1->nama = "Laptop";
    echo $produk1->nama; // Output: Laptop
    ?>
    ```

---

### Pertemuan 14: Studi Kasus - Perancangan (Mini E-commerce)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu merancang arsitektur aplikasi kecil menggunakan semua prinsip PBO yang telah dipelajari.
* **Materi Pembelajaran:** Sesi desain interaktif. Kita akan merancang sistem *back-end* e-commerce sederhana.
* **Hasil Desain (Diskusi Kelas):**
  1. **`Produk` (Abstract Class):**
     * `namespace App\Models;`
     * Properties: `protected $nama`, `protected $harga`.
     * Abstract Method: `public abstract function getInfoLengkap();`
  2. **`ProdukFisik` (Class):**
     * `namespace App\Models;`
     * `extends Produk`
     * Properties: `public $beratKg`.
     * Implementasi: `getInfoLengkap()` (menampilkan nama, harga, berat).
  3. **`ProdukDigital` (Class):**
     * `namespace App\Models;`
     * `extends Produk`
     * Properties: `public $linkDownload`.
     * Implementasi: `getInfoLengkap()` (menampilkan nama, harga, link).
  4. **`KeranjangBelanja` (Class):**
     * `namespace App\Services;`
     * Properties: `private $items = []`. (Array untuk menampung objek Produk).
     * Method: `public function tambahProduk(Produk $produk)` (Perhatikan Polymorphism di sini!).
     * Method: `public function hitungTotal()` (Looping `$items` dan menjumlahkan harga).
  5. **`Helper` (Class):**
     * `namespace App\Utils;`
     * Static Method: `public static function formatRupiah($angka)`.

---

### Pertemuan 15: Studi Kasus - Implementasi (Workshop & Proyek UAS)

* **Capaian Pembelajaran (CP-P):** Mahasiswa mampu mengimplementasikan rancangan PBO menjadi kode yang fungsional menggunakan Composer.
* **Materi Pembelajaran:** Sesi *live coding* / workshop.
  1. Dosen mendemonstrasikan setup proyek (membuat `composer.json`, `index.php`, dan `abstract class Produk`).
  2. Mahasiswa melanjutkan implementasi ini sebagai **Tugas Besar / Proyek UAS**.
  3. Fokus pada *bagaimana* semua konsep terhubung:
     * `namespace` & `autoloading` (Struktur file).
     * `new ProdukFisik(...)` (Constructor).
     * `extends Produk` (Inheritance).
     * `abstract class Produk` (Abstraksi).
     * `tambahProduk(Produk $p)` (Polymorphism).
     * `private $items` (Encapsulation).
     * `Helper::formatRupiah()` (Static Method).
  4. Proyek ini akan menjadi bahan Ujian Akhir Semester.

---

### Pertemuan 16: UJIAN AKHIR SEMESTER (UAS)

* **Bentuk:** Presentasi & Pengumpulan Proyek Studi Kasus (Mini E-commerce).
* **Penilaian:**
  * **Kebenaran Desain PBO (60%):** Apakah penggunaan `Encapsulation`, `Inheritance`, `Abstract/Interface`, dan `Polymorphism` sudah *tepat*?
  * **Kelengkapan Fungsionalitas (20%):** Apakah program berjalan sesuai fitur (tambah produk, hitung total)?
  * **Struktur Kode & Standar (20%):** Apakah menggunakan `namespace` dan `autoloading` Composer? Apakah kodenya rapi?
  * **Presentasi:** Mahasiswa mendemokan programnya dan menjelaskan *alasan desain PBO* di baliknya.
