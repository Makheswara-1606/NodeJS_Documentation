# 📖 Belajar Node.js #7 - Node.js Core Module

---

# 📌 Tujuan Pembelajaran

Setelah mempelajari materi ini saya memahami:

* Apa itu **Core Module** pada Node.js dan cara membaca dokumentasi resminya.
* Penggunaan modul bawaan **File System (`fs`)** untuk mengelola berkas.
* Perbedaan eksekusi secara **Synchronous (Blocking)** vs **Asynchronous (Non-Blocking)**.
* Penggunaan modul bawaan **Readline (`readline`)** untuk menerima input dari terminal (CLI).
* Cara menggabungkan beberapa *Core Module* untuk membuat aplikasi kontak interaktif berbasis CLI.

---

# 🧠 Apa itu Core Module?

**Core Module** adalah modul-modul resmi bawaan yang sudah tertanam langsung pada *runtime* Node.js. 

* **Karakteristik**:
  * Tidak perlu di-install via NPM.
  * Dapat langsung dipanggil menggunakan fungsi `require('nama_modul')` tanpa jalur relatif (`./`).
  * Dokumentasi lengkap tiap modul dapat diakses di [nodejs.org/docs](https://nodejs.org/docs/).

---

# 📁 1. File System (`fs`)

Modul `fs` digunakan untuk berinteraksi dengan sistem berkas komputer, seperti membuat, membaca, mengubah, atau menghapus file dan folder.

### Import Modul:
```javascript
const fs = require('fs');

```

---

## A. Menulis File (`fs.writeFileSync` vs `fs.writeFile`)

### 1. Synchronous (`writeFileSync`)

Menulis file secara langsung dan menghentikan (*blocking*) proses eksekusi kode selanjutnya hingga penulisan selesai.

```javascript
try {
  fs.writeFileSync('data/test.txt', 'Hello World secara Synchronous!');
} catch (err) {
  console.log(err);
}

```

### 2. Asynchronous (`writeFile`)

Menulis file di latar belakang (*non-blocking*) dan menggunakan fungsi *callback* yang akan dijalankan setelah proses penulisan selesai.

```javascript
fs.writeFile('data/test.txt', 'Hello World secara Asynchronous!', (err) => {
  if (err) console.log(err);
});

```

---

## B. Membaca File (`fs.readFileSync` vs `fs.readFile`)

> **Catatan**: Jika opsi encoding (`'utf-8'`) tidak disertakan, data yang dikembalikan berupa *Buffer* (biner).

### 1. Synchronous (`readFileSync`)

```javascript
const data = fs.readFileSync('data/test.txt', 'utf-8');
console.log(data);

```

### 2. Asynchronous (`readFile`)

```javascript
fs.readFile('data/test.txt', 'utf-8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

```

---

# 💬 2. Readline (`readline`)

Modul `readline` digunakan untuk membaca *stream* data input langsung dari pengguna melalui antarmuka terminal/command line.

### Import & Inisialisasi Interface:

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,   // Menerima input dari keyboard
  output: process.stdout  // Menampilkan output ke terminal
});

```

### Mengajukan Pertanyaan (`rl.question`):

```javascript
rl.question('Masukkan nama Anda: ', (nama) => {
  console.log(`Terima kasih, ${nama}`);
  
  // WAJIB ditutup agar program tidak hanging/gantung di terminal
  rl.close(); 
});

```

---

# 🛠️ Studi Kasus: Aplikasi Kontak CLI Sederhana

Menggabungkan **`readline`** (menerima input CLI) dan **`fs`** (menyimpan data ke file JSON).

### Persiapan File `data/contact.json`:

Pastikan file `data/contact.json` sudah dibuat dengan isi awal berupa *array* kosong:

```json
[]

```

### Kode Program (`app.js`):

```javascript
const fs = require('fs');
const readline = require('readline');

// Membuat interface I/O terminal
const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

// Pertanyaan 1: Nama
rl.question('Masukkan nama anda : ', (nama) => {
  // Pertanyaan 2: Nomor HP (Nested / Berantai)
  rl.question('Masukkan no hp anda : ', (noHP) => {
    
    // 1. Tampung data input ke dalam bentuk Objek
    const kontak = { nama, noHP };

    // 2. Baca file JSON yang tersimpan
    const file = fs.readFileSync('data/contact.json', 'utf8');

    // 3. Konversi string JSON menjadi Array JavaScript
    const contacts = JSON.parse(file);

    // 4. Tambahkan data kontak baru ke dalam array
    contacts.push(kontak);

    // 5. Tulis kembali Array yang sudah diperbarui ke file JSON
    fs.writeFileSync('data/contact.json', JSON.stringify(contacts));

    console.log('Terima kasih sudah memasukkan data!');
    
    // 6. Tutup koneksi readline
    rl.close();
  });
});

```

---

# 📝 Kesimpulan

Materi ini memberikan fondasi penanganan *I/O (Input/Output)* pada Node.js:

✅ **Core Module** tersedia secara bawaan tanpa perlu instalasi pihak ketiga.

✅ **Synchronous** lebih mudah dibaca untuk skrip sederhana, namun bersifat *blocking*.

✅ **Asynchronous** sangat efisien untuk operasi berat karena bersifat *non-blocking*.

✅ **`readline`** memerlukan `rl.close()` untuk mengakhiri pembacaan *stream* dari terminal.

✅ Kombinasi modul `fs` dan `readline` memungkinkan kita membuat aplikasi CLI interaktif yang menyimpan state ke dalam sistem berkas (*file system*).

---

# 📚 Istilah Penting

| Istilah | Penjelasan |
| --- | --- |
| **Core Module** | Modul resmi bawaan dari *runtime* Node.js. |
| **Buffer** | Tipe data sementara berupa biner untuk menyimpan data mentah dari I/O. |
| **`process.stdin`** | Stream bawaan yang mendengarkan ketikan keyboard pada terminal. |
| **`process.stdout`** | Stream bawaan yang menampilkan teks/output ke layar terminal. |
| **JSON.parse()** | Mengubah teks/string format JSON menjadi objek/array JavaScript. |
| **JSON.stringify()** | Mengubah objek/array JavaScript menjadi string teks format JSON. |

---

# 📖 Referensi

* Playlist **Belajar Node.js** - Web Programming UNPAS
* Video: **Belajar NodeJS | 7. NodeJS Core Module**
* Node.js Official Documentation - File System & Readline

```

```