# 📖 Belajar Node.js #5 - Menjalankan File Node

> Dokumentasi pribadi hasil belajar Node.js dari playlist **Web Programming UNPAS** oleh **Sandhika Galih**.

---

# 📌 Tujuan Pembelajaran

Setelah mempelajari materi ini saya memahami:

* Cara mengeksekusi file JavaScript di Node.js melalui terminal / command line.
* Perintah-perintah dasar terminal untuk navigasi direktori.
* Cara menggunakan Integrated Terminal di Visual Studio Code.
* Keistimewaan file `index.js` sebagai *entry point* / *root file*.
* Perbedaan skop dan perilaku variabel/fungsi di browser vs Node.js.
* Dasar penggunaan Sistem Modul (`require` dan `module.exports`).

---

# 🧠 Review Materi Sebelumnya

Pada materi sebelumnya, kita sudah belajar cara mengeksekusi JavaScript melalui **REPL** (*Read-Eval-Print Loop*) atau Node CLI secara interaktif.

Namun, untuk membangun aplikasi yang sesungguhnya, kita menulis kode JavaScript di dalam file bertipe `.js`, lalu menjalankannya menggunakan *runtime* Node.js.

---

# 💻 Persiapan & Perintah Dasar Terminal

Untuk mengeksekusi file Node.js, kita membutuhkan terminal.

* **macOS / Linux**: Terminal bawaan atau iTerm2.
* **Windows**: Sangat disarankan memakai **Git Bash** agar sintaks perintah Unix/POSIX serupa dengan Mac/Linux.

## Perintah Dasar Terminal

| Perintah | Fungsi | Contoh |
| --- | --- | --- |
| `pwd` | *Print Working Directory* (melihat posisi folder aktif) | `pwd` |
| `cd` | *Change Directory* (pindah folder) | `cd desktop` atau `cd ..` |
| `mkdir` | *Make Directory* (membuat folder baru) | `mkdir belajar-nodejs` |
| `ls` | *List* (melihat daftar file/folder dalam direktori) | `ls` |
| `clear` | Membersihkan layar terminal | `clear` |
| `code .` | Membuka folder saat ini di Visual Studio Code | `code .` |

---

# 🚀 Mengeksekusi File JavaScript dengan Node.js

## 1. Membuat & Menjalankan File
1. Buat file bernama `coba.js`.
2. Tuliskan kode JavaScript sederhana:
   ```javascript
   console.log('Hello World');

```

3. Buka terminal pada folder tempat file tersebut berada dan jalankan:
```bash
node coba.js

```


Atau tanpa menuliskan ekstensi `.js`:
```bash
node coba

```


*(Node.js secara otomatis akan mencari file dengan ekstensi `.js`)*.

## 2. Integrated Terminal di VS Code

* Tekan shortcut `Ctrl + ~` (Windows/Linux) atau `Cmd + ~` (Mac) untuk membuka/menutup terminal bawaan di VS Code.
* Pada Windows, default terminal bisa diubah menjadi **Git Bash** melalui opsi `Select Default Profile` → `Git Bash` → lalu buka *New Terminal* (`+`).

---

# 🔑 Keistimewaan File `index.js`

File bernama `index.js` secara khusus dianggap sebagai **root file** atau *entry point* utama dari sebuah project Node.js.

Jika berada di dalam direktori project, kita cukup menjalankan perintah berikut di terminal:

```bash
node .

```

Node.js secara otomatis akan mencari dan mengeksekusi file `index.js` yang ada di dalam direktori aktif tersebut.

---

# 🌐 Perilaku JavaScript: Browser vs Node.js

| Fitur / Perilaku | Browser | Node.js |
| --- | --- | --- |
| **Global Object** | Menggunakan `window` | `window` **TIDAK ADA** (`ReferenceError: window is not defined`) |
| **Keterkaitan File** | File `.js` lain yang dipanggil di HTML yang sama berbagi *scope* global | Setiap file `.js` terisolasi secara mandiri (*Module Scope*) |
| **Fitur Browser (DOM/Alert)** | Ada (`document`, `alert()`, `prompt()`) | Tidak ada |

### Contoh Kasus di Browser

Jika file `1.js` berisi fungsi `cetakNama()` dan di-*include* di HTML bersama `2.js`, maka `2.js` bisa langsung memanggil `cetakNama()` karena fungsi tersebut otomatis menempel pada objek `window`.

### Contoh Kasus di Node.js

Di Node.js, fungsi atau variabel yang dibuat di file `coba.js` **tidak bisa** langsung diakses di `index.js` begitu saja, karena Node.js menganut **Module System**.

---

# 📦 Pengenalan Sistem Modul (`require` & `module.exports`)

Node.js menganggap setiap file `.js` sebagai modul terpisah. Untuk menghubungkan atau membagikan kode antar file, digunakan fungsi `require` dan `module.exports`.

## 1. Meng-import / Menjalankan File Lain (`require`)

Untuk menjalankan isi skrip dari file `coba.js` melalui `index.js`:

```javascript
// index.js
require('./coba');

```

## 2. Mengekspor & Menggunakan Fungsi/Variabel (`module.exports`)

Agar fungsi dari `coba.js` dapat dipanggil dan dieksekusi di `index.js`:

**Langkah 1: Eksport fungsi dari `coba.js**`

```javascript
// coba.js
function cetakNama(nama) {
    return `Halo, nama saya ${nama}`;
}

// Beritahu Node.js bahwa fungsi cetakNama boleh digunakan di luar modul ini
module.exports = cetakNama;

```

**Langkah 2: Tangkap ke dalam variabel & panggil di `index.js**`

```javascript
// index.js
const cetakNama = require('./coba');

console.log(cetakNama('Sandhika Galih'));

```

---

# 📝 Kesimpulan

Materi ini menjelaskan cara mengeksekusi file JavaScript secara langsung menggunakan Node.js runtime beserta konsep dasar keterisolasian file.

Hal-hal utama yang dipelajari:

✅ Mengeksekusi file JavaScript menggunakan perintah `node <namafile>`.

✅ Menggunakan terminal terintegrasi pada VS Code untuk alur kerja yang lebih praktis.

✅ `index.js` dapat dieksekusi cukup dengan perintah `node .` sebagai file utama (*entry point*).

✅ Node.js tidak memiliki objek global `window` seperti browser.

✅ Node.js menerapkan *Module System* di mana setiap file memiliki ruang lingkup (*scope*) terisolasi.

✅ Penggunaan `require('./path')` untuk mengimpor modul dan `module.exports` untuk mengekspor fungsi/variabel.

---

# 📚 Istilah Penting

| Istilah | Penjelasan |
| --- | --- |
| **Runtime Execution** | Mengeksekusi file skrip secara langsung melalui terminal/Node.js |
| **Entry Point / Root File** | File utama tempat titik awal eksekusi aplikasi (biasanya `index.js`) |
| **Module System** | Mekanisme pengorganisasian kode ke dalam berkas-berkas terisolasi |
| **`require()`** | Fungsi bawaan Node.js untuk mengimpor file / modul lain |
| **`module.exports`** | Objek khusus Node.js untuk mengekspor variabel/fungsi keluar modul |
| **Git Bash** | Emulator terminal Unix untuk lingkungan sistem operasi Windows |

---

# 🎯 Catatan Pribadi

> Memahami cara menjalankan file dan dasar pemisahan modul via `require` serta `module.exports` adalah fondasi yang sangat penting sebelum mempelajari Sistem Modul Node.js secara lebih mendalam, manajemen paket NPM, serta pembuatan REST API dengan Express.js.

---

# 📖 Referensi

* Playlist **Belajar Node.js** - Web Programming UNPAS
* Video: **Belajar NodeJS | 5. Menjalankan File Node**
* Node.js Official Documentation - Modules

```

```