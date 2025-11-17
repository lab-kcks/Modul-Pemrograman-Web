# Modul 5 - Nuxt JS

## Pengenalan

Nuxt merupakan framework berbasis Vue yang dirancang untuk mempermudah pembuatan aplikasi web modern. Berikut adalah keunggulan utama dari Nuxt:

1. **Kemudahan Konfigurasi**: Nuxt mengurangi kerumitan konfigurasi dengan menyediakan konfigurasi bawaan yang optimal. Misalnya, manajemen routing, pengaturan webpack, serta opsimasi SEO dilakukan otomatis.

2. **Fleksibilitas Rendering**: Nuxt memiliki beberapa mode rendering yang dapat dipilih sesuai dengan kebutuhan:

    - **Server-Side Rendering (SSR)**: Aplikasi diproses di server, menghasilkan HTML lengkap yang dikirim ke browser. Mode rendering ini cocok untuk SEO dan untuk waktu _load_ halaman yang lebih cepat.

    - **Static Site Generation (SSG)**: Aplikasi di-_build_ menjadi file _static_ yang dapat langsung dihosting di _static server_ seperti Vercel atau Netlify.

    - **Client-Side Rendering (CSR)**: Mode rendering _default_ di Nuxt yang mana rendering dilakukan sepenuhnya di sisi browser.

3. **_SEO-Friendly_**: Dengan menggunakan mode rendering SSR atau SSG, Nuxt menghasilkan HTML yang lengkap sebelum dikirim ke browser, yang membantu _search engine_ untuk melakukan indeks konten lebih baik.

4. **Modularitas**: Nuxt memiliki _ecosystem_ modul yang luas. Modul seperti `@nuxt/image`, `@nuxt/auth`, atau `@nuxt/pwa` memungkinkan proses _development_ menjadi lebih cepat dengan fitur tambahan bawaan

5. **_State Management_**: Nuxt memudahkan pengelolaan data aplikasi dengan menggunakan _store_ bawaan (Vuex atau Pinia).

## Instalasi

1. Jalankan command berikut pada CLI untuk membuat proyek Nuxt:

    `npx nuxi@latest init <project-name>`

2. Setelah itu, akan ada beberapa pilihan, pilih sesuai dengan ● yang ada pada contoh dibawah ini:

    Untuk package manager, silakan pilih sesuai keinginan kalian (defaultnya adalah `npm`)

    ```
    ✔ Which package manager would you like to use?
    ○ npm
    ○ pnpm
    ○ yarn
    ○ bun
    ○ deno

    ✔ Are you interested in participating?
    ○ Yes
    ● No

    ✔ Initialize git repository?
    ● Yes
    ○ No
    ```

3. Pindah ke folder proyek (sesuai nama proyek):

    `cd <project-name>`

4. Lakukan instalasi `dependencies` yang diperlukan:

    `npm install`

5. Jalankan server `development`:

    `npm run dev`

    Aplikasi akan berjalan `http://localhost:3000` atau port lain apabila port 3000 sudah digunakan.

## _Routing_ dan Navigasi

### _File-based Routing_

Nuxt menggunakan sistem routing berbasis file/folder dalam direktori `pages/`. Berikut adalah contoh struktur foldernya:

```
pages/
--| index.vue        -> /
--| about.vue        -> /about
--| posts/
----| index.vue      -> /posts
----| _id.vue        -> /posts/:id
--| users/
----| _username.vue  -> /users/:username
```

### _Dynamic Routes_

Dibuat dengan awalan `_` (underscore) pada nama file dan untuk mengakses parameternya, bisa melalui `$route.params` dengan contoh sebagai berikut:

Path: `pages/posts/_id.vue`

```html
<template>
	<div>
		<h1>Post {{ $route.params.id }}</h1>
	</div>
</template>
```

### Navigasi

Ada dua opsi untuk mengatur navigasi di Nuxt, yaitu:

-   Menggunakan komponen `<NuxtLink>`:

    ```html
    <NuxtLink to="/about">About Page</NuxtLink>
    ```

-   Navigasi pragmatik:

    ```ts
    this.$router.push("/about");
    ```

## Komponen

Terdapat beberapa jenis komponen dalam Nuxt, yaitu:

### Komponen _Pages_

Komponen ini berada pada direktori `pages/` yang akan otomatis menjadi `route`. Komponen ini memiliki fitur khusus seperti `asyncData` dan `fetch`.

### Komponen Reguler

Komponen ini berada pada direktori `components/` yang mana akan ... `auto-import` jika terdapat konfigurasi `components: true` pada file `nuxt.config.ts`. Berikut adalah contoh komponennya:

```html
<template>
	<button class="btn">
		<slot></slot>
	</button>
</template>
```

### Komponen _Layout_

Komponen ini berada pada direktori `layouts/` dan digunakan untuk template halaman. Komponen ini ditandai dengan adanya komponent `<Nuxt />` didalamnya. Berikut adalah beberapa contoh layout:

-   _Default Layout_

    ```html
    <template>
    	<div>
    		<header>
    			<nav><!-- Navigation items --></nav>
    		</header>
    		<Nuxt />
    		<footer><!-- Footer content --></footer>
    	</div>
    </template>
    ```

-   _Custom Layout_

    Path: `layouts/blog.vue`

    ```html
    <template>
    	<div>
    		<aside><!-- Blog sidebar --></aside>
    		<Nuxt />
    	</div>
    </template>
    ```

    Path: `pages/blog.vue`

    ```ts
    export default {
    	layout: "blog",
    };
    ```

-   _Error Layout_

    Digunakan untuk menangani halaman yang tidak ditemukan (404 Not Found).

    Path: `layouts/error.vue`

    ```ts
    <template>
    	<div>
    		<h1 v-if="error.statusCode === 404">Page not found</h1>
    		<h1 v-else>An error occurred</h1>
    	</div>
    </template>;

    export default {
    	props: ["error"],
    };
    ```

### _Props_ dan _Events_

Props digunakan untuk mengirim data dari _parent component_ ke _child component_. Sebaliknya, events digunakan untuk mengirim data/sinyal dari _child component_ ke _parent component_. Berikut adalah contoh code beserta penjelasannya:

```ts
<template>
	<div @click="$emit('userSelected', user.id)">
		{{ user.name }}
	</div>
</template>

<script lang="ts">
	import { defineComponent, PropType } from 'vue';

	export default defineComponent({
		props: {
			user: {
			type: Object as PropType<{ id: number; name: string }>,
			required: true,
			},
		},
		emits: ['userSelected'],
	});
</script>
```

-   Props (`user`)

    -   Komponen tersebut menerima prop dengan nama `user`
    -   Prop dideklarasikan sebagai Object dan prop ini juga wajib diisi
    -   Bisa diakses dalam template menggunakan `user.name` dan `user.id`
    -   _Parent component_ harus memberikan data object user saat menggunakan komponen ini

-   Events (`userSelected`)
    -   Event dibuat menggunakan `$emit`
    -   Properti `@click` menandakan event akan dipanggil saat elemen di-klik
    -   `userSelected` adalah nama event yang akan diterima parent
    -   `user.id` adalah data yang dikirim ke parent melalui event
    -   _Parent_ bisa menangkap event ini dengan `@userSelected="<method-name>"`

Berikut adalah contoh penggunaan kode tersebut di _parent component_:

```ts
<template>
	<UserComponent
		:user="userData"
		@userSelected="handleUserSelection"
	/>
</template>
```

## _Data Fetching_

Nuxt menyediakan berbagai cara untuk melakukan _data fetching_ dengan mendukung SSR, SSG, dan CSR.

-   _Server-Side Rendering_

    Data diambil dari server sebelum halaman dikirimkan ke klien, sehingga memungkinkan halaman dapat di-_render_ dengan data lengkap saat pertama kali dimuat. Data fetching pada SSR dapat dilakukan menggunakan fungsi `useAsyncData`, yaitu composable bawaan Nuxt yang mendukung pengambilan data secara SSR. Berikut adalah contoh codenya:

    ```ts
    <script setup lang="ts">
    	const { data: posts, pending, error } = await useAsyncData('posts', () =>
    		$fetch('https://jsonplaceholder.typicode.com/posts')
    	);
    </script>

    <template>
    	<div>
    		<template v-if="pending">Loading...</template>
    		<template v-else-if="error">Error: {{ error.message }}</template>
    		<ul>
    		<li v-for="post in posts" :key="post.id">{{ post.title }}</li>
    		</ul>
    	</div>
    </template>
    ```

-   _Static Site Generation (SSG)_

    Data diambil selama _build time_ dan dimasukkan langsung ke file HTML statis, sehingga cocok untuk konten yang isinya jarang berubah. Untuk mengatur sebuah halaman agar menjadi statis, atur mode `static` pada `nuxt.config.ts`:

    ```ts
    export default defineNuxtConfig({
    	target: "static",
    });
    ```

    Berikut adalah contoh codenya:

    ```ts
    <script setup lang="ts">
    	const { data: products } = await useAsyncData('products', () =>
    		$fetch('https://api.example.com/products')
    	);
    </script>

    <template>
    	<div>
    		<h1>Products</h1>
    		<ul>
    			<li v-for="product in products" :key="product.id">{{ product.name }}</li>
    		</ul>
    	</div>
    </template>
    ```

-   _Client-Side Rendering_

    Data diambil di browser setelah halaman di-_render_. Biasanya digunakan untuk data yang sering berubah atau terdapat interaksi pengguna. Berikut adalah contoh codenya:

    ```ts
    <script setup lang="ts">
    	const { data: user, pending, error } = useFetch('https://api.example.com/user');
    </script>

    <template>
    	<div>
    		<template v-if="pending">Loading user data...</template>
    		<template v-else-if="error">Error: {{ error.message }}</template>
    		<p v-else>User: {{ user.name }}</p>
    	</div>
    </template>
    ```

### Komparasi SSR, SSG, dan CSR

| Metode | Kelebihan                            | Kekurangan                                    | Use Case                                |
| ------ | ------------------------------------ | --------------------------------------------- | --------------------------------------- |
| SSR    | SEO-friendly, data selalu up-to-date | Lebih lambat dibanginkan SSG                  | Dashboard, e-commerce                   |
| SSG    | Cepat, cocok untuk SEO               | Tidak cocok untuk data yang sering berubah    | Blog, dokumentasi                       |
| CSR    | Lebih interaktif, cocok untuk SPA    | Kurang optimal untuk SEO, loading awal lambat | Aplikasi internal, dashboard interaktif |

## _State Management_

State management merupakan proses mengelola data atau state yang dibutuhkan oleh berbagai bagian aplikasi untuk menjaga konsistensi dan sinkronasi. Nuxt mendukung beberapa pendekatan untuk state management, seperti Composable API dan Pinia.

-   **Composable API**

    State management bawaan dari Nuxt sehingga lebih ringan dan terintegrasi secara alami dengan Vue 3. Berikut adalah contoh penggunaannya:

    **Case: State Management untuk Counter**

    1.  Buat File Composable

        Buat file di folder `composable/`, misalnya `useCounter.ts`:

        ```ts
        export const useCounter = () => {
        	const counter = useState<number>("counter", () => 0); // State global

        	const increment = () => {
        		counter.value++;
        	};

        	const decrement = () => {
        		counter.value--;
        	};

        	return { counter, increment, decrement };
        };
        ```

    2.  Gunakan di Komponen

        ```ts
        <template>
        	<div>
        		<p>Counter: {{ counter }}</p>
        		<button @click="increment">+</button>
        		<button @click="decrement">-</button>
        	</div>
        </template>

        <script setup lang="ts">
        	import { useCounter } from '~/composables/useCounter';

        	const { counter, increment, decrement } = useCounter();
        </script>
        ```

-   Pinia

    State management resmi Vue.js yang lebih modern dibandingkan Vuex. Nuxt men-_support_ Pinia melalui modul `@pinia/nuxt`. Berikut adalah langkah-langkah untuk mengimplementasikan Pinia:

    1.  Instal Pinia

        ```bash
        npm install @pinia/nuxt
        ```

    2.  Konfigurasi `nuxt.config.ts`

        ```ts
        export default defineNuxtConfig({
        	modules: ["@pinia/nuxt"],
        });
        ```

    3.  Buat Store (Case: State Management untuk Counter)

        Buat file store di folder `stores/`, misalnya `stores/counter.ts`

        ```ts
        import { defineStore } from "pinia";

        export const useCounterStore = defineStore("counter", {
        	state: () => ({
        		counter: 0,
        	}),
        	actions: {
        		increment() {
        			this.counter++;
        		},
        		decrement() {
        			this.counter--;
        		},
        	},
        });
        ```

    4.  Gunakan di Komponen

        ```ts
        <template>
        	<div>
        		<p>Counter: {{ counter }}</p>
        		<button @click="increment">+</button>
        		<button @click="decrement">-</button>
        	</div>
        </template>

        <script setup lang="ts">
        	import { useCounterStore } from '~/stores/counter';

        	const counterStore = useCounterStore();
        	const { counter, increment, decrement } = counterStore;
        </script>
        ```
