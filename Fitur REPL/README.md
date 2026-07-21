# 📖 Belajar Node.js #4 — Node REPL (Read - Eval - Print - Loop)

> "Cara tercepat mencoba kode JavaScript tanpa harus membuat file."

---

# 🎯 Tujuan Pembelajaran

Pada materi ini kita mempelajari salah satu fitur bawaan **Node.js** yang bernama **REPL (Read - Eval - Print - Loop)**.

REPL memungkinkan kita menjalankan kode JavaScript secara **interaktif melalui Terminal atau Command Prompt** tanpa harus membuat file `.js`.

Fitur ini sangat berguna ketika ingin:

- ✅ Mencoba sintaks JavaScript
- ✅ Menguji logika program
- ✅ Melakukan debugging sederhana
- ✅ Bereksperimen dengan fungsi bawaan Node.js
- ✅ Belajar JavaScript lebih cepat

---

# 🧠 Apa itu REPL?

REPL merupakan singkatan dari:

| Singkatan | Arti | Penjelasan |
|-----------|------|------------|
| **R** | Read | Node.js membaca kode yang kita ketik |
| **E** | Eval | Node.js menjalankan atau mengevaluasi kode |
| **P** | Print | Hasil kode langsung ditampilkan |
| **L** | Loop | Node.js kembali menunggu input berikutnya |

Ilustrasinya seperti berikut.

```
User Mengetik Kode
        │
        ▼
      Read
        │
        ▼
      Eval
        │
        ▼
      Print
        │
        ▼
      Loop
        │
        └──────────────► Menunggu Input Lagi
```

Karena proses ini berlangsung terus menerus, maka dinamakan **Read - Eval - Print - Loop**.

---

# 🚀 Cara Masuk ke REPL

Buka Terminal atau Command Prompt.

Kemudian ketik

```bash
node
```

Jika berhasil maka akan muncul

```text
>
```

Artinya kita sudah berada di dalam **Node REPL**.

---

# ✨ Contoh Penggunaan

## Operasi Matematika

```javascript
10 + 20
```

Output

```text
30
```

---

## Perbandingan

```javascript
10 === "10"
```

Output

```text
false
```

---

## String

```javascript
"Belajar NodeJS"
```

Output

```text
Belajar NodeJS
```

---

## Variabel

```javascript
const nama = "Galuh"
```

Kemudian

```javascript
nama
```

Output

```text
Galuh
```

Semua variabel akan tetap tersimpan selama kita masih berada di dalam sesi REPL.

---

# 📦 Menjalankan Function

REPL juga dapat menjalankan Function.

```javascript
const sayHello = (nama) => {
    return `Halo ${nama}`
}
```

Kemudian

```javascript
sayHello("Galuh")
```

Output

```text
Halo Galuh
```

---

# 📝 Multiline Code

REPL cukup pintar untuk mengetahui apakah kode kita belum selesai.

Misalnya

```javascript
const tambah = (a, b) => {
```

Prompt akan berubah menjadi

```text
...
```

Artinya Node.js sedang menunggu kelanjutan kode.

Setelah kita menutup kurung kurawal

```javascript
}
```

Barulah kode akan dijalankan.

---

# ⌨️ History Command

Gunakan tombol keyboard berikut.

| Tombol | Fungsi |
|---------|--------|
| ⬆ | Melihat perintah sebelumnya |
| ⬇ | Melihat perintah berikutnya |

Tidak perlu mengetik ulang kode yang sama.

---

# 🌍 Global Object

Node.js memiliki object global bernama

```javascript
global
```

Object ini mirip seperti

```javascript
window
```

pada Browser JavaScript.

Untuk melihat seluruh isi global object

```javascript
global
```

Atau

```javascript
global.
```

kemudian tekan **TAB** dua kali.

---

# ⚙️ Perintah Khusus REPL

## `.help`

Menampilkan semua command REPL.

```text
.help
```

---

## `.exit`

Keluar dari REPL.

```text
.exit
```

atau

```
CTRL + C
CTRL + C
```

---

## `.break`

Membatalkan multiline code.

Misalnya kita salah mengetik function.

```javascript
const test = () => {
```

Tidak jadi melanjutkan?

Ketik

```text
.break
```

---

## `.clear`

Menghapus konteks REPL sehingga variabel dan fungsi yang dibuat dalam sesi tersebut tidak lagi tersedia.

---

## `.load`

Mengambil isi file JavaScript ke dalam REPL.

```text
.load latihan.js
```

Semua isi file akan dijalankan.

---

## `.save`

Menyimpan seluruh history REPL ke file JavaScript.

```text
.save latihan.js
```

---

## `.editor`

Masuk ke mode editor.

Mode ini lebih nyaman ketika ingin menulis kode yang terdiri dari banyak baris.

---

# 💡 Kapan REPL Digunakan?

REPL sangat cocok digunakan ketika:

- Belajar JavaScript
- Belajar Node.js
- Menguji Function
- Menguji Algoritma
- Menghitung Operasi Matematika
- Debugging
- Bereksperimen dengan API bawaan Node.js

Namun untuk membuat aplikasi sesungguhnya, sebaiknya menggunakan file `.js`.

---

# 🆚 REPL vs File JavaScript

| REPL | File JavaScript |
|------|-----------------|
| Langsung dijalankan | Harus disimpan dulu |
| Cocok untuk eksperimen | Cocok untuk project |
| Tidak permanen | Permanen |
| Cepat | Lebih terstruktur |
| Interaktif | Digunakan dalam aplikasi |

---

# 📌 Kesimpulan

Node REPL adalah **lingkungan interaktif** yang disediakan oleh Node.js untuk menjalankan kode JavaScript secara langsung melalui Terminal.

Dengan REPL kita tidak perlu membuat file setiap kali ingin mencoba kode.

REPL sangat membantu ketika:

- belajar JavaScript,
- mencoba sintaks baru,
- menguji Function,
- melakukan debugging,
- maupun memahami cara kerja Node.js.

Sedangkan ketika aplikasi mulai berkembang, barulah kode dipindahkan ke file `.js` agar lebih terstruktur dan mudah dikelola.

---

# 📚 Materi yang Dipelajari

- ✅ Apa itu Node REPL
- ✅ Cara masuk ke REPL
- ✅ Menjalankan JavaScript di Terminal
- ✅ Membuat Variabel
- ✅ Membuat Function
- ✅ Multiline Code
- ✅ History Command
- ✅ Global Object
- ✅ Command `.help`
- ✅ Command `.exit`
- ✅ Command `.break`
- ✅ Command `.clear`
- ✅ Command `.load`
- ✅ Command `.save`
- ✅ Command `.editor`

---

