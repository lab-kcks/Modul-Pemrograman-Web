# Modul 3 - Express JS dan MongoDB

## Pendahuluan

Stack (kombinasi) yang digunakan pada modul back-end ini adalah:

<p><strong>NodeJS + ExpressJS + TypeScript + PostgreSQL</strong></p>

- `NodeJS + ExpressJS`

![node_express](./images/node_express.png)

- `TypeScript`

![ts](./images/typescript.png)

- `PostgreSQL`

![postgresql](./images/postgresql.png)

## ExpressJS

**`ExpressJS`** merupakan salah satu framework nodeJS populer yang digunakan untuk membuat aplikasi web dan API. Framework ini digunakan dengan tujuan agar developer tidak perlu membuat Back-End _from scratch_ dan menghabiskan waktu mereka hanya untuk mengurus kode - kode inisiasi.

Dengan adanya framework seperti ExpressJS ini, maka developer dapat lebih berfokus pada pengerjaan _bussiness logic_ untuk aplikasi web yang akan dibuat.

### Cara Melakukan Inisiasi Project ExpressJS

Sebelum memulai proyek express, pastikan kalian telah menginstal `NodeJS` dan package manager NodeJS seperti `npm`, `yarn`, atau `pnpm`

#### **Cara Menginstal `NodeJS`**

- Download _prebuilt-installer_ NodeJS (gunakan versi yang memiliki label `LTS`) pada [link berikut](https://nodejs.org/en/download/prebuilt-installer). Nantinya akan muncul tampilan seperti di bawah ini
  ![install_node](./images/install_node.png)

- Install nodeJS melalui _prebuilt-installer_ yang sudah kalian unduh.

- Package Manager `NPM` juga akan terinstal.

- untuk memeriksa apakah `NodeJS` dan `NPM` telah terpasang, gunakan command berikut pada terminal:

  - Cek versi `NodeJS`

  ```bash
  node -v
  ```

  - Cek versi `NPM`

  ```bash
  npm -v
  ```

  ![node_npm_version](./images/node_npm_version.png)

#### **Cara Menginstal `Yarn` (Opsional)**

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

```typescript
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

## Inisiasi Prisma pada Express

### 1. Instalasi Dependencies

```bash
# Dependencies utama
npm install @prisma/client dotenv prisma
# atau
yarn add @prisma/client dotenv prisma
# atau
pnpm i @prisma/client dotenv prisma

# Untuk TypeScript (jika belum init tsconfig)
npx tsc --init
```

### 2: Inisialisasi Prisma

Jalankan perintah berikut untuk menginisialisasi Prisma:

```bash
npx prisma init
```

Perintah ini akan membuat:
- Folder `prisma/` dengan file `schema.prisma`
- File `.env` untuk environment variables

### 3. Konfigurasi Database Connection

Edit file `.env`:

```env
DATABASE_URL="postgresql://username:password@localhost:5432/modul_3?schema=public" # Sesuaikan dengan URL dari NEON Database atau PostgreSQL lokal
```

> **Catatan:** Ganti URL sesuai dengan konfigurasi masing-masing.

### 4. Membuat Schema Database

Edit file `prisma/schema.prisma`:

```typescript
// Konfigurasi generator
generator client {
  provider = "prisma-client-js"
}

// Konfigurasi datasource
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// Model User
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  name      String?
  password  String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  posts     Post[]
}

// Model Post
model Post {
  id        Int      @id @default(autoincrement())
  title     String
  content   String?
  published Boolean  @default(false)
  authorId  Int
  author    User     @relation(fields: [authorId], references: [id])
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

**Penjelasan Schema:**
- `@id`: Primary key
- `@default(autoincrement())`: Auto increment untuk ID
- `@unique`: Nilai harus unik/tidak boleh ada yang sama
- `@default(now())`: Default value timestamp saat ini
- `@updatedAt`: Otomatis update saat record diubah
- `@relation`: Mendefinisikan relasi antar tabel

### 5. Membuat Migrasi Database

```bash
npx prisma migrate dev --name init
```

Perintah ini akan:
1. Membuat file migrasi di folder `prisma/migrations`
2. Menjalankan migrasi ke database PostgreSQL
3. Generate Prisma Client

### 6. Generate Prisma Client

```bash
npx prisma generate
```

### 7. Setup Prisma Client di Project

Buat file `src/config/prisma.ts`:

```typescript
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient({
  log: ['query', 'info', 'warn', 'error'],
});

export default prisma;
```

### 8. Membuat Express Server

Buat file `src/index.ts`:

```typescript
import express, { Application, Request, Response } from 'express';
import dotenv from 'dotenv';
import prisma from './config/prisma';

// Load environment variables
dotenv.config();

const app: Application = express();
const PORT = process.env.PORT || 3000; // Sesuaikan PORT masing-masing

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Test route
app.get('/', (req: Request, res: Response) => {
  res.json({ message: 'Express + Prisma + PostgreSQL' });
});

// Start server
app.listen(PORT, () => {
  console.log(`Server berjalan di http://localhost:${PORT}`);
});

// Graceful shutdown
process.on('SIGINT', async () => {
  await prisma.$disconnect();
  console.log('Database disconnected');
  process.exit(0);
});
```

### 9. Menjalankan Aplikasi

```bash
npm run dev
```

Buka browser dan akses `localhost` sesuai dengan `PORT` masing-masing

---

## CRUD Menggunakan Prisma

### Struktur Folder Project

```
modul-4/
├── prisma/
│   ├── migrations/
│   └── schema.prisma
├── src/
│   ├── config/
│   │   └── prisma.ts
│   ├── controllers/
│   │   ├── userController.ts
│   │   └── postController.ts
│   ├── routes/
│   │   ├── userRoutes.ts
│   │   └── postRoutes.ts
│   └── index.ts
├── .env
├── package.json
└── tsconfig.json
```

### 1. CREATE - Membuat Data

#### A. User Controller

Buat file `src/controllers/userController.ts`:

```typescript
import { Request, Response } from 'express';
import prisma from '../config/prisma';

export const createUser = async (req: Request, res: Response) => {
  try {
    const { email, name, password } = req.body;

    // Validasi input
    if (!email || !password) {
      return res.status(400).json({ 
        error: 'Email dan password wajib diisi' 
      });
    }

    // Cek apakah email sudah ada
    const existingUser = await prisma.user.findUnique({
      where: { email }
    });

    if (existingUser) {
      return res.status(400).json({ 
        error: 'Email sudah terdaftar' 
      });
    }

    // Buat user baru
    const user = await prisma.user.create({
      data: {
        email,
        name,
        password // NOTE: hash password terlebih dahulu untuk real-case
      },
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true
      }
    });

    res.status(201).json({
      message: 'User berhasil dibuat',
      data: user
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat membuat user' 
    });
  }
};
```

#### B. Post Controller

Buat file `src/controllers/postController.ts`:

```typescript
import { Request, Response } from 'express';
import prisma from '../config/prisma';

export const createPost = async (req: Request, res: Response) => {
  try {
    const { title, content, authorId } = req.body;

    // Validasi input
    if (!title || !authorId) {
      return res.status(400).json({ 
        error: 'Title dan authorId wajib diisi' 
      });
    }

    // Cek apakah user ada
    const user = await prisma.user.findUnique({
      where: { id: Number(authorId) }
    });

    if (!user) {
      return res.status(404).json({ 
        error: 'User tidak ditemukan' 
      });
    }

    // Buat post baru
    const post = await prisma.post.create({
      data: {
        title,
        content,
        authorId: Number(authorId)
      },
      include: {
        author: {
          select: {
            id: true,
            name: true,
            email: true
          }
        }
      }
    });

    res.status(201).json({
      message: 'Post berhasil dibuat',
      data: post
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat membuat post' 
    });
  }
};
```

### 2. READ - Membaca Data

#### A. Get All Users

Tambahkan di `src/controllers/userController.ts`:

```typescript
export const getAllUsers = async (req: Request, res: Response) => {
  try {
    const users = await prisma.user.findMany({
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true,
        _count: {
          select: { posts: true }
        }
      }
    });

    res.json({
      message: 'Berhasil mengambil data users',
      data: users
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat mengambil data users' 
    });
  }
};
```

#### B. Get User By ID

Tambahkan di `src/controllers/userController.ts`:

```typescript
export const getUserById = async (req: Request, res: Response) => {
  try {
    const { id } = req.params;

    const user = await prisma.user.findUnique({
      where: { id: Number(id) },
      select: {
        id: true,
        email: true,
        name: true,
        createdAt: true,
        posts: {
          select: {
            id: true,
            title: true,
            published: true,
            createdAt: true
          }
        }
      }
    });

    if (!user) {
      return res.status(404).json({ 
        error: 'User tidak ditemukan' 
      });
    }

    res.json({
      message: 'Berhasil mengambil data user',
      data: user
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat mengambil data user' 
    });
  }
};
```

#### C. Get All Posts

Tambahkan di `src/controllers/postController.ts`:

```typescript
export const getAllPosts = async (req: Request, res: Response) => {
  try {
    const posts = await prisma.post.findMany({
      include: {
        author: {
          select: {
            id: true,
            name: true,
            email: true
          }
        }
      },
      orderBy: {
        createdAt: 'desc'
      }
    });

    res.json({
      message: 'Berhasil mengambil data posts',
      data: posts
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat mengambil data posts' 
    });
  }
};
```

#### D. Get Post By ID

Tambahkan di `src/controllers/postController.ts`:

```typescript
export const getPostById = async (req: Request, res: Response) => {
  try {
    const { id } = req.params;

    const post = await prisma.post.findUnique({
      where: { id: Number(id) },
      include: {
        author: {
          select: {
            id: true,
            name: true,
            email: true
          }
        }
      }
    });

    if (!post) {
      return res.status(404).json({ 
        error: 'Post tidak ditemukan' 
      });
    }

    res.json({
      message: 'Berhasil mengambil data post',
      data: post
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat mengambil data post' 
    });
  }
};
```

### 3. UPDATE - Mengubah Data

#### A. Update User

Tambahkan di `src/controllers/userController.ts`:

```typescript
export const updateUser = async (req: Request, res: Response) => {
  try {
    const { id } = req.params;
    const { email, name } = req.body;

    // Cek apakah user ada
    const existingUser = await prisma.user.findUnique({
      where: { id: Number(id) }
    });

    if (!existingUser) {
      return res.status(404).json({ 
        error: 'User tidak ditemukan' 
      });
    }

    // Update user
    const user = await prisma.user.update({
      where: { id: Number(id) },
      data: {
        ...(email && { email }),
        ...(name && { name })
      },
      select: {
        id: true,
        email: true,
        name: true,
        updatedAt: true
      }
    });

    res.json({
      message: 'User berhasil diupdate',
      data: user
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat update user' 
    });
  }
};
```

#### B. Update Post

Tambahkan di `src/controllers/postController.ts`:

```typescript
export const updatePost = async (req: Request, res: Response) => {
  try {
    const { id } = req.params;
    const { title, content, published } = req.body;

    // Cek apakah post ada
    const existingPost = await prisma.post.findUnique({
      where: { id: Number(id) }
    });

    if (!existingPost) {
      return res.status(404).json({ 
        error: 'Post tidak ditemukan' 
      });
    }

    // Update post
    const post = await prisma.post.update({
      where: { id: Number(id) },
      data: {
        ...(title && { title }),
        ...(content !== undefined && { content }),
        ...(published !== undefined && { published })
      },
      include: {
        author: {
          select: {
            id: true,
            name: true,
            email: true
          }
        }
      }
    });

    res.json({
      message: 'Post berhasil diupdate',
      data: post
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat update post' 
    });
  }
};
```

### 4. DELETE - Menghapus Data

#### A. Delete User

Tambahkan di `src/controllers/userController.ts`:

```typescript
export const deleteUser = async (req: Request, res: Response) => {
  try {
    const { id } = req.params;

    // Cek apakah user ada
    const existingUser = await prisma.user.findUnique({
      where: { id: Number(id) },
      include: {
        _count: {
          select: { posts: true }
        }
      }
    });

    if (!existingUser) {
      return res.status(404).json({ 
        error: 'User tidak ditemukan' 
      });
    }

    // Hapus semua post user terlebih dahulu (cascade delete)
    await prisma.post.deleteMany({
      where: { authorId: Number(id) }
    });

    // Hapus user
    await prisma.user.delete({
      where: { id: Number(id) }
    });

    res.json({
      message: 'User berhasil dihapus'
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat menghapus user' 
    });
  }
};
```

#### B. Delete Post

Tambahkan di `src/controllers/postController.ts`:

```typescript
export const deletePost = async (req: Request, res: Response) => {
  try {
    const { id } = req.params;

    // Cek apakah post ada
    const existingPost = await prisma.post.findUnique({
      where: { id: Number(id) }
    });

    if (!existingPost) {
      return res.status(404).json({ 
        error: 'Post tidak ditemukan' 
      });
    }

    // Hapus post
    await prisma.post.delete({
      where: { id: Number(id) }
    });

    res.json({
      message: 'Post berhasil dihapus'
    });
  } catch (error) {
    console.error(error);
    res.status(500).json({ 
      error: 'Terjadi kesalahan saat menghapus post' 
    });
  }
};
```

### 5. Setup Routes

#### A. User Routes

Buat file `src/routes/userRoutes.ts`:

```typescript
import { Router } from 'express';
import {
  createUser,
  getAllUsers,
  getUserById,
  updateUser,
  deleteUser
} from '../controllers/userController';

const router = Router();

router.post('/', createUser);
router.get('/', getAllUsers);
router.get('/:id', getUserById);
router.put('/:id', updateUser);
router.delete('/:id', deleteUser);

export default router;
```

#### B. Post Routes

Buat file `src/routes/postRoutes.ts`:

```typescript
import { Router } from 'express';
import {
  createPost,
  getAllPosts,
  getPostById,
  updatePost,
  deletePost
} from '../controllers/postController';

const router = Router();

router.post('/', createPost);
router.get('/', getAllPosts);
router.get('/:id', getPostById);
router.put('/:id', updatePost);
router.delete('/:id', deletePost);

export default router;
```

### 6. Update Main Server

Edit file `src/index.ts`:

```typescript
import express, { Application, Request, Response } from 'express';
import dotenv from 'dotenv';
import prisma from './config/prisma';
import userRoutes from './routes/userRoutes';
import postRoutes from './routes/postRoutes';

// Load environment variables
dotenv.config();

const app: Application = express();
const PORT = process.env.PORT || 3000;

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.get('/', (req: Request, res: Response) => {
  res.json({ 
    message: 'Express + Prisma + PostgreSQL API',
    endpoints: {
      users: '/api/users',
      posts: '/api/posts'
    }
  });
});

app.use('/api/users', userRoutes);
app.use('/api/posts', postRoutes);

// 404 handler
app.use((req: Request, res: Response) => {
  res.status(404).json({ error: 'Endpoint tidak ditemukan' });
});

// Start server
app.listen(PORT, () => {
  console.log(`Server berjalan di http://localhost:${PORT}`);
});

// Graceful shutdown
process.on('SIGINT', async () => {
  await prisma.$disconnect();
  console.log('Database disconnected');
  process.exit(0);
});
```

## Referensi

- [Prisma Documentation](https://www.prisma.io/docs)

- [Express.js Documentation](https://expressjs.com/)

- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

- [TypeScript Documentation](https://www.typescriptlang.org/docs/)

- Berikut link download Postman untuk melakukan testing API (sangat disarankan dan sangat membantu)
  https://www.postman.com/downloads/

- Atau apabila tidak ingin mendownload, gunakan Hoppscotch https://hoppscotch.io/ atau apidog https://apidog.com/api-doc/
