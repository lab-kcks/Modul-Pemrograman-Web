# Modul 4 - React JS

# React JS

## Javascript XML (JSX) and JS Difference

lorem

## Virtual DOM

lorem

## How to init React Project

lorem

## Component and Props

lorem

## Event Handling

lorem

## Conditional Rendering

lorem

## Render List and Key List

lorem

## Hooks

lorem

## Fetch API

lorem

## Route (React Router)

lorem

# Tailwind CSS

## Introduction

Tailwind CSS adalah sebuah framework CSS untuk mempermudah styling dan layouting website. Dengan Tailwind, styling dapat dilakukan dengan class-class atau kode tertentu untuk mengatur tampilan website mulai dari warna, ukuran, margin, padding, dan lainnya tanpa perlu melakukan defining CSS _from scratch_. Sehingga, untuk melakukan styling hanya perlu menambahkan kelas-kelas pada HTML sesuai kebutuhan.

![with-without-tailwind](./assets/with-without-tailwind.png)

## Instalasi Tailwind CSS pada React

Setelah melakukan init project React, perlu dilakukan langkah-langkah berikut untuk integrasi Tailwind CSS pada project React yang telah di-init.

1. Melakukan instalasi tailwindcss dan dependecies-nya.

```bash
npm install tailwindcss @tailwindcss/vite
```

2. Tambahkan konfigurasi `@tailwindcss/vite` pada file konfigurasi Vite `vite.config.js`.

```javascript
import { defineConfig } from "vite";
import tailwindcss from "@tailwindcss/vite";

export default defineConfig({
	plugins: [tailwindcss()],
});
```

4. Tambahkan `@tailwind` directives pada file CSS pada project React.

```css
@import "tailwindcss";
```

5. Start project React

```bash
npm run dev
```

## Contoh penggunaan Tailwind CSS pada React

```jsx
import React from "react";

export default function HelloWorld() {
	return (
		<main>
			<p className="text-white text-5xl font-bold text-center py-96">
				Hello World
			</p>
		</main>
	);
}
```

![Tailwind Example](./assets/tailwind-example.png)

## Dokumentasi Tailwind CSS

Untuk dokumentasi yang lebih jelas dapat melihat source resmi dari Tailwind CSS berikut.

**[TailwindCSS installation](https://tailwindcss.com/docs/installation/using-vite)**

## Dokumentasi Tailwind CSS

Untuk dokumentasi yang lebih jelas dapat melihat source resmi dari Tailwind CSS berikut.

**[TailwindCSS installation](https://tailwindcss.com/docs/installation/using-vite)**

Untuk mempelajari dan menggunakan Tailwind CSS, bisa menuju ke link documentation resmi dari Tailwind CSS berikut karena documentation yang diberikan sudah sangat lengkap dan mencakup hampir keseluruhan penggunaan Tailwind CSS.

**[Dokumentasi Tailwind CSS](https://tailwindcss.com/docs/installation)**
