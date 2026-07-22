# 📖 Belajar Node.js #6 - Node.js Module System

---

# 📌 Tujuan Pembelajaran

Setelah mempelajari materi ini saya memahami:

* Konsep dasar **Module System** pada Node.js.
* Perbedaan skop/ruang lingkup (*scope*) antara browser dan Node.js.
* Tiga jenis modul utama di Node.js (**Core**, **Local**, dan **Third-Party**).
* Urutan pencarian (*resolving mechanism*) ketika fungsi `require()` dipanggil.
* Cara mengekspor fungsi, variabel, objek, dan kelas menggunakan `module.exports`.
* Cara mengimpor dan menggunakan modul lokal dengan sintaks ES6 Object Short Notation.

---

# 🧠 Review & Konsep Dasar Module

## Apa itu Module?
* **Secara Umum**: Sekumpulan kode terorganisir yang dapat digunakan kembali (*reusable*) dengan antarmuka (*interface*) yang jelas.
* **Di Node.js**: Setiap file JavaScript (`.js`) dianggap sebagai satu modul yang terisolasi (*isolated scope*). Kode di dalam satu modul **tidak mencemari global scope** dan tidak bisa diakses file lain secara bebas tanpa mekanisme ekspor dan impor.


```

+------------------+         require()         +------------------+
|   coba.js        |  ──────────────────────>  |   index.js       |
| (Local Module)   |  <──────────────────────  |  (Main Entry)    |
+------------------+     module.exports        +------------------+

```

---

# 🧩 3 Jenis Module di Node.js

Node.js membagi modul menjadi 3 kelompok utama:

| Jenis Modul | Deskripsi | Contoh |
| --- | --- | --- |
| **Core Modules** | Modul resmi bawaan runtime Node.js, langsung bisa dipakai tanpa installasi. | `fs`, `http`, `path`, `os` |
| **Local Modules** | Modul buatan sendiri yang berada di dalam folder project lokal. | `./coba.js`, `./utils/math.js` |
| **Third-Party Modules** | Modul buatan komunitas yang di-install via **NPM** dan disimpan di `node_modules`. | `express`, `moment`, `mongoose` |

---

# 🔍 Urutan Pencarian `require()`

Ketika dipanggil perintah `require('x')`, Node.js akan melakukan pencarian sesuai urutan hirarki berikut:

1. **Core Module**: Mengecek apakah `'x'` adalah nama modul bawaan Node.js.
2. **Local Module**: Jika menggunakan relatif path (seperti `./x` atau `../x`), Node.js mencari berkas lokal tersebut.
3. **Third-Party Module**: Jika bukan keduanya, Node.js secara otomatis mencari folder bernama `'x'` di dalam direktori `node_modules`.

---

# 💻 Praktik Membuat & Mengekspor Local Module

## 1. Membuat Modul (`coba.js`)
Kita dapat membuat berbagai jenis tipe data (fungsi, variabel, objek, hingga kelas) di dalam satu berkas modul:

```javascript
// coba.js

// 1. Fungsi
function cetakNama(nama) {
    return `Halo, nama saya ${nama}`;
}

// 2. Variabel / Konstanta
const PI = 3.14;

// 3. Objek
const mahasiswa = {
    nama: 'Dodi',
    umur: 20,
    cetakMhs() {
        return `Halo, nama saya ${this.nama}, umur saya ${this.umur} tahun.`;
    }
};

// 4. Kelas
class Orang {
    constructor() {
        console.log('Objek Orang telah diinstansiasi!!');
    }
}

```

---

## 2. Cara Mengekspor Modul (`module.exports`)

### A. Ekspor Properti demi Properti (Bertahap)

```javascript
module.exports.cetakNama = cetakNama;
module.exports.PI = PI;
module.exports.mahasiswa = mahasiswa;
module.exports.Orang = Orang;

```

### B. Ekspor Sekaligus (Dianjurkan - ES6 Object Short Notation)

Jika nama properti sama dengan nama nilai/variabelnya, kita cukup menuliskan nama variabelnya saja di dalam objek ekspor:

```javascript
module.exports = {
    cetakNama,
    PI,
    mahasiswa,
    Orang
};

```

---

## 3. Mengimpor & Menggunakan Modul (`index.js`)

Di berkas utama (`index.js`), kita memanggil modul lokal menggunakan relative path (`./coba`):

```javascript
// index.js
const coba = require('./coba');

// 1. Memanggil Fungsi
console.log(coba.cetakNama('Sandhika Galih'));

// 2. Memanggil Variabel / Properti
console.log(coba.PI);

// 3. Memanggil Method dari Objek
console.log(coba.mahasiswa.cetakMhs());

// 4. Menginstansiasi Kelas
const orang1 = new coba.Orang();

```

---

# 📝 Kesimpulan

Materi ini menjelaskan fondasi pengorganisasian kode dalam ekosistem Node.js:

✅ Setiap file `.js` pada Node.js adalah modul mandiri yang terisolasi dari lingkup global.

✅ Menggunakan `module.exports` untuk menentukan variabel/fungsi mana yang boleh diakses dari luar modul.

✅ Menggunakan `require()` untuk membawa masuk modul lain ke dalam berkas aktif.

✅ Penggunaan ES6 Short Notation membuat sintaks ekspor objek menjadi lebih ringkas dan bersih.

✅ Memahami perbedaan struktur impor antara **Core Modules**, **Local Modules**, dan **Third-Party Modules**.

---

# 📚 Istilah Penting

| Istilah | Penjelasan |
| --- | --- |
| **Module Scope** | Batas ruang lingkup variabel/fungsi yang hanya terisolasi di dalam file itu sendiri. |
| **`module.exports`** | Objek khusus di Node.js yang digunakan untuk membagikan isi modul ke luar. |
| **`require()`** | Fungsi built-in Node.js untuk mengimpor dan mengeksekusi modul lain. |
| **Core Module** | Modul standar/bawaan dari Node.js. |
| **Third-Party Module** | Modul eksternal dari komunitas yang dikelola via NPM. |
| **Object Short Notation** | Fitur ES6 untuk menulis properti objek dengan ringkas jika nama kunci & variabel nilainya sama. |

---

# 🎯 Catatan Pribadi

> Konsep pemisahan modul merupakan kunci utama sebelum melangkah ke materi **Core Modules** (seperti File System/`fs`) dan penggunaan **NPM / Express.js**. Struktur pemisahan kode ini menjaga aplikasi skala besar tetap rapi, modular, dan mudah di-maintain.

---

# 📖 Referensi

* Playlist **Belajar Node.js** - Web Programming UNPAS
* Video: **Belajar NodeJS | 6. NodeJS Module System**
* Node.js Official Documentation - Modules API

```

```