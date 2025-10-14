# Modul 3 - Express JS dan MongoDB

## Pendahuluan

Stack (kombinasi) yang digunakan pada modul back-end ini adalah:

<p><strong>NodeJS + ExpressJS + TypeScript + Prisma ORM + PostgreSQL</strong></p>

- `NodeJS + ExpressJS`

![node_express](./images/node_express.png)

- `TypeScript`

![ts](./images/typescript.png)

- `PostgreSQL`

![postgre](./images/psql.jpg)

## ExpressJS

**`ExpressJS`** merupakan salah satu framework nodeJS populer yang digunakan untuk membuat aplikasi web dan API. Framework ini digunakan dengan tujuan agar developer tidak perlu membuat Back-End _from scratch_ dan menghabiskan waktu mereka hanya untuk mengurus kode - kode inisiasi.

Dengan adanya framework seperti ExpressJS ini, maka developer dapat lebih berfokus pada pengerjaan _bussiness logic_ untuk aplikasi web yang akan dibuat.

### Cara Melakukan Inisiasi Project ExpressJS

Sebelum memulai proyek express, pastikan kalian telah menginstal `NodeJS` dan package manager NodeJS seperti `npm`, `yarn`, atau `pnpm`

#### **Cara Menginstal `Yarn` (Opsional)**

Pada modul sebelumnya, kita telah mengetahui cara menginstal NODE JS. Setelah menginstalnya, kita juga mendapat sebuah package manager yang disebut dengan `NPM`. Kali ini, kita akan mencoba menginstal package manager yang lain.

Menginstal Package Manager `Yarn` dapat dilakukan dengan menggunakan perintah dari `NPM`.

- Jalankan command berikut pada terminal:

  ```bash
  npm install -g yarn
  ```

  > Catatan: flag `-g` perlu digunakan agar yarn dapat digunakan di lokasi manapun pada komputer kalian.

- Periksa versi yarn menggunakan perintah berikut:

  ```bash
  yarn -v
  ```

  ![yarn_version](./images/yarn_version.png)

#### **Cara Menginstal `PNPM` (Opsional)**

Menginstal Package Manager `PNPM` dapat dilakukan dengan menggunakan perintah dari `NPM`.

- Jalankan command berikut pada terminal:

  ```bash
  npm install -g pnpm
  ```

  > Catatan: flag `-g` perlu digunakan agar pnpm dapat digunakan di lokasi manapun pada komputer kalian.

- Periksa versi pnpm menggunakan perintah berikut:

  ```bash
  pnpm -v
  ```

  ![pnpm_version](./images/pnpm_version.png)

#### **Inisiasi Proyek ExpressJS + TypeScript**

Pada bagian ini akkan dijelaskan bagaimana cara melakukan setup project Express + TypeScript. Perhatikan langkah - langkahnya.

1. Buka terminal pada IDE kalian, kemudian mulai inisiasi proyek menggunakan `Package Manager` pilihan kalian.

```bash
# Menggunakan NPM
npm init

# Menggunakan yarn
yarn init

# Menggunakan PNPM
pnpm init
```

Jawab pertanyaan yang diberikan. Jawaban dari pertanyaan tidak akan memengaruhi hasil dari proyek. hasilnya akan tampak seperti berikut:

![yarn_init](./images/yarn_init.png)

> **`Tambahan`**: buat file `.gitignore` kemudian isi dengan teks `node_modules` agar folder node_module tidak ikut masuk ke github.

2. Instal dependensi `ExpressJS`

```bash
# Menggunakan NPM
npm install express

# Menggunakan yarn
yarn add express

# Menggunakan PNPM
pnpm i express
```

3. Instal juga dependensi `typescript`, `@types/node`, `ts-node`, `nodemon` dan `@types/express` kali ini dengan flag `-D`

```bash
# Menggunakan NPM
npm install -D typescript @types/node @types/express ts-node nodemon

# Menggunakan yarn
yarn add -D typescript @types/node @types/express ts-node nodemon

# Menggunakan PNPM
pnpm i -D typescript @types/node @types/express ts-node nodemon
```

> Dependencies merupakan list package yang diperlukan oleh aplikasi untuk berjalan (pada tahap production), sementara devDependencies merupakan list package yang digunakan khusus pada saat tahap pengembangan (development) atau testing

4. Buat file `tsconfig.json` untuk mengatur compiler typescript

```bash
npx tsc --init
```

Nantinya akan muncul sebuah file bernama `tsconfig.json` yang isinya berbagai macam konfigurasi yang dapat digunakan pada compiler typescript nantinya.

Namun untuk mempermudah pengaturan, kalian bisa hapus semua isi dari file `tsconfig.json` kemudian isi dengan pengaturan di bawah ini

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "declaration": true,
    "removeComments": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "allowSyntheticDefaultImports": true,
    "target": "ES2021",
    "sourceMap": true,
    "noEmit": false,
    "outDir": "./dist",
    "baseUrl": "./src",
    "skipLibCheck": true,
    "strict": true,
    "strictNullChecks": false,
    "noImplicitAny": true,
    "strictBindCallApply": true,
    "forceConsistentCasingInFileNames": false,
    "noFallthroughCasesInSwitch": false,
    "strictPropertyInitialization": false,
    "esModuleInterop": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true
  }
}
```

5. Buat folder bernama `src` kemudian buat pula file di dalam src dengan nama `index.ts`

Struktur direktori saat ini seharusnya berbentuk seperti pada di bawah ini.

```
./
├───node_modules/
├───src/
│     index.ts
│
│ package.json
│ yarn.lock
```

> file yarn.lock akan berbeda - beda sesuai dengan package manager yang kalian gunakan

6. Lakukan inisiasi express pada file `index.ts`. file ini akan menjadi file utama kita pada proyek ini

```javascript
import express from "express";

const app = express();

app.use(express.json());

// check endpoint
app.get("/", (_, response) => {
  response.status(200).send("Server is up and running 💫");
});

const PORT = 4000;
app.listen(PORT, () => {
  console.log(`Express is running on Port ${PORT}`);
});
```

7. Siapkan script untuk menjalankan website.

Pada file `package.json`, tambahkan script sesuai dengan teks di bawah agar website dapat dijalankan.

```json
"scripts": {
  "build": "tsc --build",
  "start": "node ./dist/index.js",
  "start:dev": "nodemon ./src/index.ts"
},
```

Hasilnya akan tampak seperti ini

![pckg_json](./images/pckg_json.png)

8. Jalankan website dengan command berikut

```bash
# Menggunakan NPM
npm run start:dev

# Menggunakan yarn
yarn start:dev

# Menggunakan PNPM
pnpm start:dev
```

9. Buka website kalian pada `http://localhost:PORT` dengan `PORT` merupakan nilai PORT yang sudah kalian deklarasikan pada file `index.ts`

![init_result](./images/init_result.png)

10. Selamat, kalian telah membuat endpoint pertama kalian menggunakan `ExpressJS + TypeScript`

11. Script `build` dan `start` merupakan command yang digunakan pada tahap production, namun modul ini tidak akan membahas expressJS pada tahap production.

### Express Router

Express Router adalah cara untuk memisahkan dan mengorganisasi rute API dalam aplikasi Express. Dengan menggunakan Router, kita dapat membuat endpoint yang lebih terstruktur dan modular, memungkinkan kita untuk mengelompokkan rute berdasarkan fungsionalitas, misalnya rute untuk "users" atau "products."

Dari proyek yang sudah kita buat sebelumnya, kali ini kita akan mengubah strukturnya menjadi `Function Based Structure`.

1. Buat folder `router` pada `src` kemudian isi dengan file `index.ts` dan `food.router.ts`

Strukturnya akan tampak seperti berikut:

```
./
├───node_modules/
├───src/
│     ├───router/
│     │   ├─food.router.ts
│     │   │ index.ts
│     │
│     │ index.ts
│
│ package.json
│ yarn.lock
```

2. Selanjutnya, kita akan isi `food.router.ts` dengan beberapa endpoint

```typescript
import express from "express";

const router = express.Router();

router.get("/pizza", (_, res) => {
  res.status(200).send("Mmm... Pizza... 🍕");
});

router.get("/cookie", (_, res) => {
  res.status(200).send("Get some Cookie... 🍪");
});

router.get("/donut", (_, res) => {
  res.status(200).send("Do Not... 🍩");
});

export default router;
```

3. Panggil food router yang sudah dibuat sebelumnya pada file `router/index.ts`

```typescript
import express from "express";
const router = express.Router();

import foodRouter from "./food.router";

router.use("/food", foodRouter);

export default router;
```

4. Terakhir, gunakan router sebelumnya pada file `src/index.ts` dengan mengubah sebagian dari isinya

```typescript
import express from "express";
import router from "./router"; // import routernya

const app = express();

app.use(express.json());

// check endpoint
app.get("/", (_, response) => {
  response.status(200).send("Server is up and running 💫");
});

app.use(router); // tambahkan baris ini untuk menggunakan router

const PORT = 4000;
app.listen(PORT, () => {
  console.log(`Express is running on Port ${PORT}`);
});
```

5. Sekarang apabila kalian menjalankan websitenya, kalian akan mendapati beberapa endpoint baru.

![new_router](./images/new_router.png)

Selain `Get`, express juga mendukung berbagai metode lain seperti `Post`, `Patch`, `Put`, dan `Delete`. Berikut untuk lebih jelasnya.

#### **`GET`**

Metode GET digunakan untuk mengambil data dari server. Biasanya, metode ini digunakan untuk membaca atau mengakses data yang tersedia.

Contoh Kode:

```typescript
// Rute GET untuk mendapatkan semua data pengguna
router.get("/users", (req: Request, res: Response) => {
  res.status(200).json({ message: "Retrieve all users" });
});

// Rute GET untuk mendapatkan data spesifik dari pengguna berdasarkan ID
router.get("/users/:id", (req: Request, res: Response) => {
  const { id } = req.params;
  res.status(200).json({ message: `Retrieve user with ID: ${id}` });
});
```

#### **`POST`**

Metode POST digunakan untuk mengirim data baru ke server, biasanya digunakan untuk menambah data baru.

Contoh Kode:

```typescript
// Rute POST untuk menambah pengguna baru
router.post("/users", (req: Request, res: Response) => {
  const { name, email } = req.body;
  res.status(201).json({ message: "User created", data: { name, email } });
});
```

#### **`PATCH`**

Metode PATCH digunakan untuk memperbarui sebagian data pada sumber daya yang ada. Metode ini digunakan ketika kita hanya ingin memperbarui sebagian dari data.

Contoh Kode:

```typescript
// Rute PATCH untuk memperbarui sebagian data pengguna berdasarkan ID
router.patch("/users/:id", (req: Request, res: Response) => {
  const { id } = req.params;
  const { email } = req.body;
  res
    .status(200)
    .json({ message: `User with ID: ${id} updated`, data: { email } });
});
```

#### **`PUT`**

Metode PUT digunakan untuk memperbarui data secara menyeluruh pada sumber daya yang ada. Semua data biasanya ditimpa dengan data baru yang dikirimkan.

Contoh Kode:

```typescript
// Rute PUT untuk memperbarui data pengguna secara menyeluruh berdasarkan ID
router.put("/users/:id", (req: Request, res: Response) => {
  const { id } = req.params;
  const { name, email } = req.body;
  res
    .status(200)
    .json({ message: `User with ID: ${id} replaced`, data: { name, email } });
});
```

#### **`DELETE`**

Metode DELETE digunakan untuk menghapus data dari server.

Contoh Kode:

```typescript
// Rute DELETE untuk menghapus pengguna berdasarkan ID
router.delete("/users/:id", (req: Request, res: Response) => {
  const { id } = req.params;
  res.status(200).json({ message: `User with ID: ${id} deleted` });
});
```

### Express Request

Pada `Express`, objek **Request** digunakan untuk **menyimpan semua informasi yang dikirimkan** oleh klien saat mengakses endpoint tertentu. Objek ini memiliki berbagai properti yang memungkinkan kita untuk mengakses data yang dikirimkan, seperti header, parameter, body, dan query.

#### **Request Head**

Request Head atau header permintaan adalah metadata yang dikirimkan dari klien ke server dalam bentuk key-value pair. Header ini dapat digunakan untuk memberikan informasi tambahan seperti jenis konten (Content-Type), otorisasi (Authorization), atau custom header lainnya.

Contoh Kode:

```typescript
router.get("/headers", (req: Request, res: Response) => {
  const contentType = req.headers["content-type"];
  const authorization = req.headers["authorization"];

  res.status(200).json({
    message: "Headers received",
    headers: { contentType, authorization },
  });
});
```

#### **Request Body**

Request Body berisi data yang dikirimkan oleh klien ke server, biasanya melalui metode POST, PUT, atau PATCH. Body umumnya berisi data yang ingin disimpan atau diperbarui, seperti data pengguna atau data formulir.

Contoh Kode:

```typescript
router.post("/data", (req: Request, res: Response) => {
  const { name, email } = req.body;

  res.status(201).json({
    message: "Data received",
    data: {
      name,
      email,
    },
  });
});
```

#### **Request Param**

Request Param digunakan untuk mengambil data dari URL yang bersifat dinamis, biasanya pada bagian path. Data ini sering digunakan untuk menentukan sumber daya spesifik, seperti ID pengguna atau produk.

Contoh Kode:

```typescript
router.get("/users/:id", (req: Request, res: Response) => {
  const { id } = req.params;

  res.status(200).json({
    message: `User with ID: ${id} found`,
  });
});
```

#### **Request Query**

Request Query digunakan untuk mendapatkan parameter tambahan dari URL, biasanya untuk menambahkan filter atau opsi tambahan dalam permintaan. Query parameters ditambahkan setelah tanda ? di URL dan sering digunakan untuk menentukan opsi seperti pencarian atau pagination.

Contoh Kode:

```typescript
router.get("/search", (req: Request, res: Response) => {
  const { keyword, page, limit } = req.query;

  res.status(200).json({
    message: "Search results",
    filters: {
      keyword,
      page: Number(page),
      limit: Number(limit),
    },
  });
});
```

### Express Response

objek Response digunakan untuk mengirimkan respons dari server ke klien setelah permintaan diproses. Melalui objek ini, kita dapat menentukan data apa yang akan dikembalikan, status kode HTTP, tipe konten, serta mengatur header lain yang dibutuhkan klien. Menggunakan Response, kita juga dapat mengirimkan respons dalam berbagai format, seperti JSON, HTML, atau teks biasa.

#### **Http Status Code**

Kode status HTTP adalah angka yang menunjukkan status hasil permintaan klien. Kode ini membantu klien memahami apakah permintaan berhasil, dialihkan, atau mengalami error. Berikut adalah beberapa kategori utama kode status HTTP yang sering digunakan:

- Code `2XX`:

  Kode status 2XX menunjukkan bahwa **permintaan berhasil**. Kode ini digunakan saat data dikirimkan dengan benar atau saat operasi selesai dengan sukses. Contoh kode 2XX yang sering digunakan adalah `200 OK`, `201 Created`, dan `204 No Content`.

- Code `3XX`:

  Kode status 3XX digunakan untuk mengindikasikan bahwa **permintaan harus dialihkan ke lokasi lain**. Ini sering digunakan untuk redirect, seperti saat konten berpindah ke URL baru. Contoh kode 3XX yang sering digunakan adalah `301 Moved Permanently`, `302 Found`, dan `304 Not Modified`.

- Code `4XX`:

  Kode status 4XX menunjukkan **kesalahan di sisi klien**. Kode ini berarti bahwa permintaan tidak dapat diproses karena masalah yang disebabkan oleh klien, seperti kesalahan autentikasi atau data yang tidak valid. Contoh kode 4XX yang sering digunakan adalah `400 Bad Request`, `401 Unauthorized`, dan `404 Not Found`.

- Code `5XX`:

  Kode status 5XX menunjukkan bahwa terjadi **kesalahan di sisi server**. Hal ini biasanya berarti bahwa server tidak dapat memenuhi permintaan karena masalah internal atau gangguan pada server. Contoh kode 5XX yang sering digunakan adalah `500 Internal Server Error`, `502 Bad Gateway`, dan `503 Service Unavailable`.

#### **Cara Membuat Response yang Sesuai**

Response yang baik berarti memiliki informasi yang lengkap dan mudah untuk dibaca. Umumnya response selalu dikembalikan dalam bentuk `JSON` yang isinya seperti berikut:

- `message`: string yang menjelaskan response tersebut. Misalkan `success get all user data` atau `user not found`

- `status`: Boolean (true / false) yang menunjukkan apakah permintaan berhasil atau tidak. Status seharusnya sudah direpresentasikan dalam bentuk kode HTTP, namun karena variasi kode HTTP sangat banyak, maka status ini berfungsi untuk mengerucutkannya menjadi tanda sukses atau tidak.

- `data`: Objek yang berisi semua data yang diminta klien

- `metadata (opsional)`: Metadata biasanya digunakan pada permintaan yang memiliki pagination dan sejenisnya. Metadata menunjukkan bagaimana kondisi data yang diberikan.

## PostgreSQL

## Neon Database

## Prisma ORM

### Pendahuluan

lorem

### Mengapa Menggunakan Prisma ORM?

lorem

### Inisiasi Prisma pada Express

lorem

### CRUD Menggunakan Prisma

lorem

### Filtering & Pagination

lorem

### Aggregate function

lorem

### Transaction & Batch Queries

lorem

### Raw Query menggunakan Prisma

lorem

## Aplikasi Testing API

- Berikut link download Postman untuk melakukan testing API (sangat disarankan dan sangat membantu).
  https://www.postman.com/downloads/

- Atau apabila tidak ingin mendownload, gunakan Hoppscotch. https://hoppscotch.io/

- Untuk dokumentasi yang lebih jelas bisa langsung menuju ke website resmi MongoDB berikut.
  https://www.mongodb.com/resources/languages/express-mongodb-rest-api-tutorial
