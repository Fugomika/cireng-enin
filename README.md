# Website Cireng Enin 🧡

Website satu halaman untuk promosi Cireng Enin. Tidak perlu install apa-apa —
cukup buka `index.html` di browser.

```
cireng/
├── index.html    ← seluruh website (tampilan + isi + pengaturan)
├── images/       ← foto-foto menu
└── README.md     ← file ini
```

## Cara mengubah isi website

Semua yang sering berubah (nomor WhatsApp, harga, menu) ada di **satu tempat**:
buka `index.html` dengan editor teks apa pun (Notepad, TextEdit, VS Code),
lalu cari tulisan besar:

```
PENGATURAN CIRENG ENIN — CUKUP EDIT BAGIAN INI SAJA! ✏️
```

Di bawahnya ada blok `PENGATURAN`. Hanya bagian itu yang perlu disentuh.

### 1. Ganti nomor WhatsApp

```js
nomorWA: "6281234567890",        // format internasional, TANPA + dan tanpa spasi
nomorTampil: "+62 812-3456-7890" // yang tampil di halaman, bebas formatnya
```

Contoh: nomor `0812-9999-8888` → `nomorWA: "6281299998888"`
(angka 0 di depan diganti 62).

### 2. Ganti harga atau nama menu

Setiap menu berbentuk seperti ini — tinggal ubah teksnya:

```js
{
  nama: "Cireng Ayam Full",
  deskripsi: "Satu box penuh cireng persegi isi ayam suwir...",
  harga: "Rp 40.000",
  satuan: "1 box · 10 pcs + saos",
  gambar: "images/ayam-full.svg",
  favorit: true   // true = muncul pita "Favorit!", false = tidak
},
```

- **Menambah menu:** salin satu blok `{ ... },` lalu tempel di bawahnya dan ubah isinya.
- **Menghapus menu:** hapus satu blok `{ ... },` utuh (termasuk koma di belakangnya).

### 3. Ganti foto menu

Sebagian menu masih memakai gambar contoh (file `.svg` di folder `images/`);
Mix 3 Rasa dan Stik Bawang sudah pakai foto asli. Untuk memakai foto asli:

1. Foto cireng dengan pencahayaan terang (dekat jendela siang hari paling bagus),
   posisi agak melebar (landscape).
2. Simpan file foto ke folder `images/`, misalnya `ayam.jpg`.
3. Di blok menu, ubah baris gambarnya:
   `gambar: "images/ayam.jpg"`

Usahakan ukuran file di bawah ±300 KB supaya website tetap cepat
(bisa dikecilkan gratis di [squoosh.app](https://squoosh.app)).

### 4. Ganti Instagram dan area layanan

```js
instagram: "cireng.enin",              // tanpa @
area: "Kota Bandung & sekitarnya",
```

### 5. Ganti pesan WhatsApp otomatis

```js
pesanUmum: "Halo Cireng Enin! 😊 Saya mau pesan cireng...",
```

Ini pesan yang otomatis terisi saat pembeli klik tombol "Pesan Sekarang".

## Cara melihat hasilnya

Klik dua kali `index.html` — website terbuka di browser. Setelah mengedit,
simpan file lalu refresh browser (tekan `Cmd+R` / `F5`).

## Cara menaruh website di internet (gratis)

Cara paling gampang: [Netlify Drop](https://app.netlify.com/drop) —
seret seluruh folder `cireng` ke halaman itu, selesai. Dapat alamat
seperti `cireng-enin.netlify.app` yang bisa dibagikan di Instagram/WhatsApp.

Alternatif: GitHub Pages, Vercel, atau Cloudflare Pages — semuanya gratis
untuk website statis seperti ini.
