# 📖 Belajar Node.js #2 - Arsitektur Node.js

> Dokumentasi pribadi hasil belajar Node.js dari playlist **Web Programming UNPAS** oleh **Sandhika Galih**.

---

# 📌 Tujuan Pembelajaran

Setelah mempelajari materi ini saya memahami:

* Apa itu arsitektur Node.js.
* Mengapa Node.js menggunakan JavaScript tetapi berbeda dengan JavaScript di Browser.
* Cara kerja Node.js secara **Single Thread**, **Asynchronous**, dan **Non-Blocking**.
* Perbedaan kode **Synchronous** dan **Asynchronous**.
* Mengapa Callback diperlukan.
* Alasan Node.js mampu menangani banyak request secara efisien.

---

# 🧠 Review Materi Sebelumnya

Node.js adalah **JavaScript Runtime Environment**.

Artinya Node.js memungkinkan JavaScript berjalan **di luar Browser**.

JavaScript dijalankan menggunakan **Google V8 Engine**, yaitu JavaScript Engine yang digunakan oleh Google Chrome.

```
JavaScript
      │
      ▼
 Google V8 Engine
      │
      ▼
    Node.js
```

---

# 🌍 JavaScript di Browser vs Node.js

## JavaScript di Browser

Saat JavaScript dijalankan di browser, JavaScript mempunyai akses terhadap seluruh fitur browser.

Contohnya:

* DOM
* HTML
* CSS
* Window
* History
* Location
* Alert
* Prompt
* Confirm

Contoh:

```javascript
document.getElementById("judul");

document.querySelector(".card");

window.location.href;
```

Semua kode di atas hanya dapat berjalan karena JavaScript berada di dalam Browser.

---

## JavaScript di Node.js

Node.js **tidak memiliki Browser**.

Sehingga object seperti:

* document
* window
* history
* alert()

tidak tersedia.

Sebagai gantinya Node.js dapat mengakses:

* File System
* Operating System
* Network
* HTTP
* Process
* Path
* Buffer

Contohnya:

```javascript
const fs = require("fs");
```

atau

```javascript
const os = require("os");
```

Node.js dapat:

* membaca file
* membuat file
* membuat server
* menghapus file
* mengetahui sistem operasi
* membaca environment variable
* membuat API

---

# 🔥 Kenapa Node.js Memilih V8?

Setiap browser memiliki JavaScript Engine masing-masing.

| Browser               | JavaScript Engine |
| --------------------- | ----------------- |
| Google Chrome         | V8                |
| Mozilla Firefox       | SpiderMonkey      |
| Microsoft Edge (lama) | Chakra            |

Node.js menggunakan **V8 Engine** karena:

* Sangat cepat.
* Dioptimalkan oleh Google.
* Menggunakan Just In Time Compilation.
* Performa tinggi untuk menjalankan JavaScript.

---

# ⚙️ Arsitektur Node.js

Node.js memiliki tiga karakter utama.

```
Single Thread
Asynchronous
Non Blocking
```

Ketiga konsep inilah yang membuat Node.js sangat cepat.

---

# 1️⃣ Single Thread

Node.js hanya mempunyai **satu Main Thread**.

Artinya:

```
Program
   │
   ▼
Main Thread
```

Semua JavaScript dijalankan oleh thread tersebut.

Berbeda dengan bahasa yang membuat banyak thread untuk setiap request.

---

# 2️⃣ Asynchronous

Asynchronous berarti:

Program **tidak perlu menunggu** proses sebelumnya selesai.

Misalnya:

```
Request Data A
Request Data B
Cetak Hello World
```

Walaupun Data A belum selesai, program tetap lanjut mengerjakan proses berikutnya.

---

# 3️⃣ Non Blocking

Non Blocking berarti:

Program **tidak berhenti** hanya karena ada satu proses yang membutuhkan waktu lama.

Misalnya:

```
Download File
```

selama download berlangsung,

program tetap dapat:

* menerima request lain
* membaca file lain
* menjalankan fungsi lain

---

# 🍽️ Ilustrasi Restoran

Sandhika Galih menggunakan ilustrasi restoran.

## Cara Kerja Synchronous

```
Customer 1
      │
      ▼
Waiter
      │
      ▼
Dapur
      │
      ▼
Customer selesai

baru...

Customer 2
```

Semua customer harus menunggu satu sama lain.

---

## Cara Kerja Asynchronous

```
Customer 1
      │
      ▼
Waiter
      │
      ▼
Dapur

(waiter langsung kembali)

Customer 2
      │
      ▼
Waiter
      │
      ▼
Dapur

(waiter kembali lagi)

Customer 3
```

Waiter tidak perlu menunggu makanan selesai.

Inilah konsep Node.js.

---

# 📊 Perbedaan Synchronous vs Asynchronous

## Synchronous

```
Request User 1
↓

Menunggu...

↓

Request User 2

↓

Menunggu...

↓

Hello World
```

Output:

```
User 1
User 2
Hello World
```

Semuanya berjalan berurutan.

---

## Asynchronous

```
Request User 1

↓

Request User 2

↓

Hello World

↓

User 2

↓

User 1
```

Output:

```
Hello World
User 2
User 1
```

Program tidak menunggu request selesai.

---

# 🔄 Callback

Agar proses asynchronous dapat dijalankan ketika selesai, digunakan **Callback**.

Contoh sederhana:

```javascript
getUser(id, function(user) {
    console.log(user);
});
```

atau menggunakan Arrow Function

```javascript
getUser(id, (user) => {
    console.log(user);
});
```

Artinya:

> Jalankan fungsi ini setelah proses `getUser()` selesai.

---

# ⏳ Simulasi setTimeout()

Pada video digunakan `setTimeout()` untuk mensimulasikan proses yang lama.

```javascript
setTimeout(() => {

    console.log("Data selesai");

},3000);
```

3000 berarti:

```
3000 ms

=

3 detik
```

---

# 📌 Ilustrasi Timeline

Misalnya terdapat:

```
Request User 1
(3 detik)

Request User 2
(2 detik)

Hello World
```

Maka hasilnya:

```
0 detik
↓

Hello World

↓

2 detik

User 2

↓

3 detik

User 1
```

Inilah contoh nyata **Non Blocking**.

---

# 💡 Kelebihan Node.js

Karena menggunakan model asynchronous dan non-blocking, Node.js cocok untuk:

* REST API
* Backend Website
* Chat Application
* Realtime Notification
* Streaming
* Multiplayer Game Server
* Microservice
* IoT
* WebSocket

---

# ❌ Kesalahan Umum Pemula

Banyak pemula mengira Node.js bisa menggunakan:

```javascript
document.getElementById();
```

atau

```javascript
window.location;
```

Padahal Node.js **tidak berjalan di Browser**.

Karena itu object tersebut tidak tersedia.

---

# 📝 Kesimpulan

Materi ini menjelaskan fondasi paling penting dalam belajar Node.js.

Hal-hal yang saya pelajari:

✅ Node.js menggunakan Google V8 Engine.

✅ Node.js berjalan di luar Browser.

✅ Tidak memiliki DOM maupun Window.

✅ Memiliki akses ke File System dan Operating System.

✅ Menggunakan konsep Single Thread.

✅ Bersifat Asynchronous.

✅ Bersifat Non Blocking.

✅ Callback digunakan untuk menjalankan kode setelah proses asynchronous selesai.

Konsep-konsep ini akan menjadi dasar sebelum mempelajari:

* Module Node.js
* File System (fs)
* HTTP Server
* Express.js
* Database
* REST API
* Promise
* Async Await
* Event Loop

---

# 📚 Istilah Penting

| Istilah             | Penjelasan                                       |
| ------------------- | ------------------------------------------------ |
| Runtime Environment | Lingkungan untuk menjalankan JavaScript          |
| V8 Engine           | Mesin JavaScript milik Google                    |
| Single Thread       | Hanya memiliki satu thread utama                 |
| Asynchronous        | Tidak menunggu proses selesai                    |
| Non Blocking        | Proses lain tetap berjalan                       |
| Callback            | Fungsi yang dijalankan setelah proses selesai    |
| File System         | Modul untuk mengakses file                       |
| Event Loop          | Mekanisme Node.js mengelola operasi asynchronous |

---

# 🎯 Catatan Pribadi

> Sebelum belajar Express.js atau framework backend lainnya, saya harus benar-benar memahami konsep **Single Thread**, **Asynchronous**, **Non-Blocking**, **Callback**, dan nantinya **Promise** serta **Async/Await**. Semua konsep tersebut merupakan fondasi utama dalam pengembangan backend menggunakan Node.js.

---

# 📖 Referensi

* Playlist **Belajar Node.js** - Web Programming UNPAS
* Video: **Belajar NodeJS #2 - Arsitektur NodeJS**
* Google V8 Engine Documentation
* Node.js Official Documentation
