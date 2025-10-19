# Modul 4 - React
<img width="512" height="256" alt="reactjs_logo_icon_170805" src="https://github.com/user-attachments/assets/c6ed785f-a056-4478-be32-38fdba21e4ca" />

Selamat datang di React! Di modul ini, kita akan berkenalan dengan *library* JavaScript paling populer untuk membangun *User Interface* (UI) yang interaktif dan efisien.

---
## 1. Prasyarat: Cek Instalasi Node.js

Sebelum kita bisa membuat proyek React, kita **wajib** memiliki Node.js. Kenapa? Karena kita membutuhkan **NPM** (Node Package Manager) untuk mengunduh *package* React dan menjalankan server pengembangan.

Buka terminal Anda dan jalankan dua perintah ini:

```bash
node -v
npm -v
```

Jika sudah terinstal, akan menunjukkan versi dari node dan npm

<img width="299" height="143" alt="image" src="https://github.com/user-attachments/assets/ddcda6fc-2412-475a-9cbf-c1ab39cec573" />

Jika belum terinstal, silahkan instal node seperti yang ada di **modul 2**

## 2. Apa itu React & Mengapa Pakai?

### 2.1 Apa itu React?
Secara sederhana, **React** adalah *library* (pustaka) JavaScript yang dibuat oleh Facebook untuk membangun antarmuka pengguna (UI).

Pikirkan React seperti **kotak mainan LEGO digital**. Daripada membangun seluruh halaman web sebagai satu kesatuan besar, React membiarkan kita membangunnya dari potongan-potongan kecil yang disebut **Komponen**.

Anda bisa membuat komponen `Tombol`, komponen `Navbar`, komponen `FormInput`, lalu menggabungkan semua "LEGO" tersebut untuk membuat aplikasi web yang utuh.



### 2.2 Mengapa Harus Pakai React?
1.  **Berbasis Komponen**: Membuat kode jadi **reusable** (bisa dipakai ulang), lebih rapi, dan mudah dikelola. Mau 10 tombol di halaman? Cukup panggil komponen `Tombol` 10 kali.
2.  **Deklaratif**: Kita cukup memberi tahu React **apa** yang kita inginkan tampil di layar (misal: "tampilkan nama pengguna"), dan React yang akan mengurus *bagaimana* cara menampilkannya. Ini lebih sederhana daripada JavaScript biasa (imperatif) di mana kita harus memberi instruksi langkah demi langkah (`document.getElementById(...)`, `innerHTML = ...`).
3.  **Cepat dan Efisien**: Ini adalah alasan terbesarnya. React menggunakan teknologi canggih bernama **Virtual DOM** (akan kita bahas selanjutnya) yang membuat aplikasi terasa sangat cepat dan responsif.

---

## 3. JSX (JavaScript XML) vs. JS

Saat pertama kali melihat React, Anda akan menemukan sintaks yang terlihat seperti HTML di dalam file JavaScript. Ini disebut **JSX**.

* **JavaScript (JS) Murni**
    Jika kita ingin membuat `<h1>` dengan JS murni (menggunakan React), kodenya akan terlihat seperti ini. Cukup merepotkan.
    ```javascript
    const element = React.createElement(
      'h1',
      { className: 'judul' },
      'Halo, Praktikan!'
    );
    ```

* **JSX (JavaScript XML)**
    JSX adalah "gula sintaksis" (*syntactic sugar*) yang mempermudah penulisan. Kode di atas bisa kita tulis seperti ini:
    ```jsx
    const element = <h1 className="judul">Halo, Praktikan!</h1>;
    ```
    Jauh lebih mudah dibaca, bukan?

**Poin Penting:** Browser **tidak mengerti JSX**. Di belakang layar, *compiler* (seperti Babel atau Vite) akan mengubah kode JSX Anda yang cantik itu kembali menjadi kode `React.createElement()` yang bisa dimengerti oleh JavaScript.

---

## 4. Apa itu Virtual DOM? 

Ini adalah salah satu konsep "sihir" di balik kecepatan React.

* **Masalah:** Memanipulasi **DOM Asli** (Real DOM) di browser itu sangat **lambat** dan "mahal" secara sumber daya. Bayangkan Anda harus merenovasi seluruh rumah hanya untuk mengganti satu ubin.

* **Solusi React:** **Virtual DOM (VDOM)**.

Virtual DOM adalah **salinan** atau **cetak biru (blueprint) ringan** dari DOM asli yang disimpan oleh React di dalam memori.



Prosesnya begini:
1.  Saat ada data berubah (misal: Anda mengetik di *form*), React akan membuat **cetak biru baru** di Virtual DOM.
2.  React membandingkan cetak biru baru ini dengan cetak biru lama (proses ini disebut **"diffing"**). Ini super cepat karena terjadi di memori, bukan di browser.
3.  React menemukan, "Oh, ternyata yang berubah cuma teks di paragraf ini."
4.  React kemudian **hanya mengubah satu paragraf itu saja** di DOM Asli. Proses ini disebut **"reconciliation"**.

**Analogi:** Daripada merenovasi seluruh rumah (Real DOM), React membandingkan denah lama dan denah baru (Virtual DOM), lalu hanya menyuruh tukang untuk memindahkan satu kursi yang berbeda (Reconciliation).

---

## 5. Cara Inisiasi Proyek React 🚀

Cara tercepat dan paling modern untuk memulai proyek React adalah menggunakan *build tool* bernama **Vite** (dibaca "vit").

Ikuti langkah-langkah ini di terminal Anda:

1.  **Jalankan Perintah Create Vite**
    Pastikan Anda berada di direktori tempat Anda ingin menyimpan proyek (misal `Documents/`).
    ```bash
    npm create vite@latest
    ```

2.  **Ikuti Petunjuknya**
    Vite akan menanyakan beberapa hal. Jawab seperti ini:
    * **Project name:** `...` (Isi nama proyek Anda, misal: `latihan-react`)
    * **Select a framework:** `...` (Gunakan panah, pilih **React**)
    * **Select a variant:** `...` (Gunakan panah, pilih **TypeScript**)
    * **Install with npm and start now?** `...` (Pilih **Yes**)

3.  **Proses Otomatis & Buka di Browser**
    Setelah Anda memilih "Yes", Vite akan secara otomatis melakukan semua langkah untuk Anda:
    * Membuat folder proyek.
    * Menjalankan `npm install` (mengunduh semua *package*).
    * Menjalankan `npm run dev` (menyalakan server pengembangan).

    Anda tidak perlu lagi mengetik `cd ...` atau `npm install` secara manual.

    Terminal akan langsung memberi Anda URL (biasanya `http://localhost:5173/`). Buka alamat itu di browser, dan Anda akan melihat proyek React pertama Anda berjalan!
	<img width="1919" height="900" alt="image" src="https://github.com/user-attachments/assets/06336072-295e-4174-9f5a-a06cf398bc15" />
