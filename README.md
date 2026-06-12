# ⌥ GitCMS Blog — Platform Blog Berbasis GitHub

Blog statis lengkap dengan CMS terintegrasi, berjalan **100% di atas GitHub** — tanpa database, tanpa server, tanpa biaya hosting.

Tulis artikel di panel admin → konten tersimpan sebagai Markdown di repo Anda → GitHub Actions otomatis membangun situs statis yang **SEO-friendly** → publikasi ke GitHub Pages.

```
┌──────────────┐   tulis    ┌──────────────┐  commit   ┌──────────────┐
│  Panel Admin │ ─────────► │ content/*.md │ ────────► │ GitHub Repo  │
│   (/admin/)  │            │  (Markdown)  │           └──────┬───────┘
└──────────────┘            └──────────────┘                  │ push
                                                               ▼
┌──────────────┐  deploy   ┌──────────────┐   build    ┌──────────────┐
│ GitHub Pages │ ◄──────── │   _site/     │ ◄───────── │GitHub Actions│
│ (blog live)  │           │ (HTML statis)│            │  (build.js)  │
└──────────────┘           └──────────────┘            └──────────────┘
```

---

## ✨ Fitur

**Blog publik (SEO-optimized):**
- 🚀 Halaman statis murni — sangat cepat, skor Lighthouse tinggi
- 🔍 Meta tag lengkap: `description`, canonical, **Open Graph**, **Twitter Card**
- 📊 **Structured data JSON-LD** (BlogPosting, WebSite, BreadcrumbList)
- 🗺️ **sitemap.xml** & **RSS feed** otomatis
- 🏷️ Halaman arsip per **kategori** dan **tag**
- 📄 Paginasi, artikel terkait, halaman statis (Tentang, dll)
- 🌗 Mode terang & gelap otomatis
- 📱 Responsif penuh — header mobile dengan menu hamburger & **submenu dropdown** (desktop) / accordion (mobile)
- 🧩 **Widget footer** — Teks/HTML, Artikel Terbaru, Daftar Kategori, Tag Populer, Media Sosial
- 🖼️ **Logo & favicon** kustom, ikon **SVG** untuk tautan media sosial

**Panel admin (CMS):**
- 🔐 Login via GitHub Personal Access Token
- ✍️ Editor Markdown dengan preview & toolbar
- 📝 Metadata lengkap: judul, slug, kategori, tag, excerpt, featured image, status
- 📚 **Modul Artikel** dengan paginasi 20 per halaman (urut terbaru → lama)
- 📄 **Modul Halaman** — kelola halaman statis (Tentang, Kontak, dll) langsung dari CMS
- 🏷️ **Modul Kategori** — kelola daftar kategori + deskripsi (disimpan di `content/categories.json`)
- ☰ **Modul Menu Navigasi** — atur item menu header (tambah/urutkan/hapus) tanpa edit kode
- 🔗 **Slug bersih** — URL artikel berbentuk `domain.com/slug-artikel` (URL lama `/posts/…` otomatis dialihkan)
- 🖼️ Upload & kelola gambar
- ☰ **Modul Menu Navigasi** — atur item menu header + **submenu bertingkat** (tambah/urutkan/hapus) tanpa edit kode
- 🧩 **Modul Widget** — kelola blok footer (disimpan di `content/widgets.json`)
- 🖼️ Upload, kelola, & **hapus** gambar (dengan konfirmasi)
- 🎨 **Modul Tema** — pilih tema aktif & atur opsinya (warna aksen, font) langsung dari CMS
- ⚙️ **Editor pengaturan situs** — judul, deskripsi, sosial media, **logo, favicon, teks copyright footer**
- 🔔 Konfirmasi sebelum menghapus artikel, halaman, kategori, widget, & media
- 🔍 Pencarian artikel & halaman

---

## 🚀 Panduan Instalasi

### 1. Upload ke Repository GitHub

Buat repo baru (mis. `blog-cms`), lalu unggah seluruh isi folder ini.

```bash
git init
git add .
git commit -m "Initial commit: GitCMS Blog"
git branch -M main
git remote add origin https://github.com/USERNAME/blog-cms.git
git push -u origin main
```

### 2. Sesuaikan `config.json`

**PENTING** — edit minimal dua baris ini agar URL situs benar:

```json
{
  "baseUrl": "https://USERNAME.github.io/blog-cms",
  "basePath": "/blog-cms"
}
```

| Jenis situs | `baseUrl` | `basePath` |
|---|---|---|
| Project site (umum) | `https://user.github.io/blog-cms` | `/blog-cms` |
| User site | `https://user.github.io` | `` (kosong) |
| Domain sendiri | `https://blogsaya.com` | `` (kosong) |

> Anda juga bisa mengubah ini nanti lewat menu **Pengaturan Situs** di panel admin.

### 3. Aktifkan GitHub Pages

1. Repo → **Settings → Pages**
2. **Source**: pilih **GitHub Actions**
3. Buka tab **Actions**, tunggu workflow *Build and Deploy Blog* selesai (±1–2 menit)
4. Blog Anda live di `baseUrl` yang Anda set

### 4. Buat Personal Access Token

1. `https://github.com/settings/tokens` → **Fine-grained tokens** → **Generate new token**
2. **Repository access** → *Only select repositories* → pilih repo blog Anda
3. **Repository permissions** → **Contents** → **Read and write**
4. Generate, lalu **salin token**

### 5. Login & Mulai Menulis

1. Buka `<baseUrl>/admin/` (mis. `https://USERNAME.github.io/blog-cms/admin/`)
2. Tempel token → isi konfigurasi repo (owner, repo, branch `main`, folder `content/posts`)
3. Tulis artikel → **Simpan & Commit**
4. Tunggu ±1 menit, artikel muncul di blog publik 🎉

---

## 🔄 Alur Publikasi

```
Edit di /admin/  →  commit ke content/posts/  →  Actions build  →  Pages update
```

Setiap kali Anda menyimpan artikel atau mengubah pengaturan, GitHub Actions otomatis membangun ulang situs. Mirip "Publish" di WordPress, tapi tanpa server.

---

## 📁 Struktur Folder

```
blog-cms/
├── admin/                  ← panel CMS (akses di /admin/)
│   ├── index.html
│   └── assets/{css,js}/
├── content/
│   ├── posts/              ← artikel blog (.md) ← DIKELOLA CMS
│   └── pages/              ← halaman statis (about.md, dll)
├── themes/                 ← KUMPULAN TEMA (tampilan situs)
│   └── default/            ← tema bawaan
│       ├── theme.json      ← manifest + opsi tema (warna, font)
│       ├── assets/         ← style.css & script.js tema
│       └── templates/      ← template HTML (fungsi murni → HTML)
│           ├── home.js · post.js · page.js · archive.js · not-found.js
│           └── partials/   ← head, header, footer, layout, post-card, icons
├── build/                  ← INTI (engine) — stabil, jarang disentuh
│   ├── build.js            ← orkestrator static site generator
│   ├── theme.js            ← pemuat tema (baca config.theme)
│   ├── seo.js              ← penghasil metadata & JSON-LD
│   ├── util.js             ← helper bersama (slug, URL, tanggal)
│   └── serve.js            ← server pratinjau lokal
├── public/images/          ← gambar yang diunggah
├── config.json             ← konfigurasi situs (+ "theme" & "themeOptions")
├── package.json            ← dependensi build
├── .github/workflows/
│   └── deploy.yml          ← pipeline build & deploy
└── _site/                  ← hasil build (auto-generate, tidak di-commit)
```

> **Pemisahan inti vs tema.** `build/` (engine) menyediakan **data**; `themes/<nama>/` memutuskan **tampilan**. Mengganti tema cukup mengubah satu field `theme` di `config.json` — inti tidak perlu disentuh.

---

## 💻 Pratinjau Lokal (Opsional)

Untuk menguji sebelum push (butuh Node.js 18+):

```bash
npm install      # sekali saja
npm run build    # bangun situs ke _site/
npm run serve    # jalankan di http://localhost:4321
```

Buka `http://localhost:4321/blog-cms/` (sesuai `basePath`) untuk melihat blog,
dan `/admin/` untuk panel CMS.

---

## 📝 Format Artikel

Setiap artikel = file Markdown dengan frontmatter:

```markdown
---
title: "Judul Artikel"
slug: judul-artikel
date: 2026-06-05
status: published        # atau "draft" (tidak ditampilkan)
category: "SEO"
author: "Nama Anda"
tags: ["seo", "tutorial"]
excerpt: "Ringkasan untuk SEO & kartu artikel."
featured_image: "/public/images/foto.jpg"
---

## Isi artikel dalam Markdown
```

---

## 🎨 Kustomisasi

| Ingin mengubah… | Edit file… |
|---|---|
| Warna, font, tampilan | `themes/default/assets/style.css` (variabel CSS di `:root`) atau menu **Tema** |
| Pilih / ganti tema | `config.json` → field `theme`, atau menu **Tema** |
| Opsi tema (warna aksen, font) | `config.json` → `themeOptions`, atau menu **Tema** |
| Judul, deskripsi, sosmed | `config.json` atau menu **Pengaturan Situs** |
| Menu navigasi | `config.json` → bagian `nav` |
| Struktur halaman (HTML) | `themes/default/templates/*.js` |
| Meta tag & JSON-LD (SEO) | `build/seo.js` (inti) + `themes/default/templates/partials/head.js` |
| Logika build | `build/build.js` (inti) |

---

## 🧩 Sistem Tema

GitCMS memisahkan **inti** dari **tampilan**, mirip tema WordPress.

- **Inti (`build/`)** membaca konten, menghitung SEO, dan menyiapkan *data*. Ia tidak tahu seperti apa HTML-nya.
- **Tema (`themes/<nama>/`)** menerima data itu lewat satu objek `ctx` dan mengembalikan HTML.

**Kontrak:** *inti menyediakan data, tema memutuskan tampilannya.* Tema **tidak boleh** menyentuh GitHub API, filesystem, logika slug/permalink, sitemap, atau RSS — semua itu milik inti.

### Tema bawaan

| Tema (`theme`) | Untuk | Beranda |
|---|---|---|
| `default` | Blog / publikasi | Daftar artikel + hero sederhana |
| `company` | **Company profile** | **Landing page**: hero, statistik, layanan, tentang, wawasan terbaru, CTA band |

Tema **Company Profile** bertipografi *Bricolage Grotesque* + *Hanken Grotesk* dengan gaya minimalis korporat (banyak ruang putih, garis tipis, satu aksen). Beranda landing-nya membaca objek opsional **`config.profile`**:

```json
"profile": {
  "eyebrow": "Profil Perusahaan",
  "headline": "Solusi digital untuk pertumbuhan bisnis Anda",
  "subheadline": "Satu kalimat pendukung di bawah judul hero.",
  "heroBackground": "/public/images/hero.jpg",
  "heroImage": "",
  "primaryCta":   { "text": "Hubungi Kami", "url": "/about/" },
  "secondaryCta": { "text": "Lihat Layanan", "url": "#layanan" },
  "stats":    [ { "value": "120+", "label": "Proyek Selesai" } ],
  "services": [ { "icon": "layers", "title": "Pengembangan Web", "text": "…" } ],
  "about":    { "title": "Tentang Kami", "text": "…", "image": "", "points": ["…"] },
  "ctaBand":  { "title": "Siap mulai?", "text": "…", "button": { "text": "Hubungi Kami", "url": "/about/" } },
  "sidebar":  [ { "type": "cta", "title": "Konsultasi Gratis", "text": "…", "button": { "text": "Hubungi", "url": "/about/" } } ]
}
```

Setiap seksi hanya tampil bila datanya diisi; bila `profile` kosong, beranda otomatis memakai `title`/`description`. Nilai `icon` yang tersedia: `spark, layers, chart, shield, chat, rocket, globe, gear, pen, target, clock, users, check`. Objek `profile` bersifat aditif — diabaikan oleh tema `default`.

**Foto di beranda.** Semua foto memakai path dari panel **Media** (tombol *Salin path*, mis. `public/images/nama.jpg`):
- `heroBackground` — foto **latar** hero (full-bleed) dengan overlay otomatis agar teks terbaca. Bila diisi, hero memakai mode latar foto (teks rata-tengah, warna terang).
- `heroImage` — foto **di samping** hero (hero jadi dua kolom). Hanya dipakai bila `heroBackground` kosong.
- `about.image` — foto pada seksi *Tentang* (bila kosong, tampil panel dekoratif).

**Sidebar halaman dalam.** `config.profile.sidebar` adalah daftar blok yang muncul di **semua halaman selain beranda** (halaman statis, artikel, arsip). Bila kosong, halaman tampil lebar penuh. Tipe blok:

| `type` | Field |
|---|---|
| `text` | `title`, `content` (HTML) |
| `cta` | `title`, `text`, `button{ text, url }` |
| `links` | `title`, `items[ { label, url } ]` |
| `recent-posts` | `title`, `count` |
| `contact` | `title`, `text` (memakai `social.email`) |
| `image` | `src`, `alt`, `caption`, `link` |
| `social` | `title` (memakai `social`) |

### Menu **Sesuaikan** (Customize) — editor berbasis skema

Mulai versi ini, tampilan publik **sepenuhnya ditangani tema** dan diatur lewat menu **Sesuaikan** — Anda tidak perlu lagi menyunting `config.json` secara manual. Polanya meniru **Appearance → Customize** di WordPress:

- Menu **Tema** = galeri tema (kartu). Klik **Aktifkan** untuk berganti tema, atau **Sesuaikan →** untuk mengaturnya.
- Menu **Sesuaikan** = form penyesuaian untuk **tema aktif**, dibangun otomatis dari skema di `theme.json`.

Setiap tema mendeklarasikan blok **`customize`** di `theme.json`. Admin membaca skema itu dan merender form-nya sendiri — **tanpa kode khusus per tema di inti**:

```json
"customize": {
  "options": {
    "accent": { "type": "color", "label": "Warna Aksen", "default": "#1f7a4d" }
  },
  "sections": [
    {
      "id": "hero", "label": "Hero", "icon": "✦",
      "fields": [
        { "key": "headline", "type": "text", "label": "Judul Hero" },
        { "key": "heroBackground", "type": "image", "label": "Foto Latar" },
        { "key": "primaryCta", "type": "group", "label": "Tombol Utama", "fields": [
          { "key": "text", "type": "text", "label": "Teks" },
          { "key": "url",  "type": "text", "label": "URL" }
        ] },
        { "key": "stats", "type": "repeater", "label": "Statistik", "fields": [
          { "key": "value", "type": "text", "label": "Angka" },
          { "key": "label", "type": "text", "label": "Keterangan" }
        ] }
      ]
    }
  ]
}
```

**Tipe field yang didukung:** `text`, `textarea`, `number`, `select` (`choices`), `color`, `checkbox`, `image` (pemilih Media + Upload), `note` (teks bantu), `group` (pembungkus visual; `key` jadi awalan jalur bersarang, mis. `primaryCta.text`), `linklist` (textarea `Label | URL` → array `{label,url}`), dan `repeater` (daftar berulang). Repeater bisa berisi objek (`fields`), **string biasa** (`itemType:"string"`, mis. daftar poin), atau **blok bertipe** (`typeField` + `variants`, mis. sidebar yang tiap bloknya beda field).

Kunci field mendukung **jalur bertitik** untuk menyimpan nilai bersarang (mis. `"key": "about.points"`, `"key": "ctaBand.button.url"`). Bagian khusus **Tampilan** (jika ada `customize.options`) mengatur CSS variable tema.

> Tombol **Simpan Penyesuaian** menulis ke `config.themeData["<tema>"]` (lihat di bawah). Untuk **tema aktif**, nilainya juga di-*mirror* ke `config.profile`/`config.themeOptions` agar build & template tema membacanya seperti biasa. Tema tanpa blok `customize` (mis. `default` yang minimalis) menampilkan pesan "tidak ada opsi penyesuaian" — tampilannya tetap statis.

### Penyimpanan per-tema (`config.themeData`)

Agar **banyak tema** hidup berdampingan tanpa saling menimpa, data tiap tema disimpan terpisah — mirip *theme_mods* WordPress:

```json
"themeData": {
  "company": { "options": { "accent": "#1f7a4d" }, "content": { "headline": "…", "stats": [ … ] } },
  "default":  { "options": {}, "content": {} }
}
```

Berganti tema **mengarsipkan** data tema lama ke `themeData` dan memuat data tema baru — jadi konten company profile Anda tetap utuh saat mencoba tema lain, lalu kembali lagi. Field lama (`profile`, `themeOptions`) tetap ada sebagai **cermin tema aktif** demi kompatibilitas mundur: `config.json` lama tetap nge-build sama persis tanpa perubahan apa pun.

### Membuat tema baru

1. Salin `themes/default/` → `themes/<nama-baru>/`.
2. Sesuaikan `assets/style.css` dan template di `templates/`.
3. Perbarui `theme.json` (nama, versi). Tambahkan blok **`customize`** agar tema bisa diatur dari menu **Sesuaikan**: `options` untuk CSS variable (dibaca via `ctx.themeVars`) dan `sections[].fields[]` untuk konten. Lihat **[CUSTOMIZER.md](CUSTOMIZER.md)** untuk daftar lengkap tipe field. Inti & admin **tidak perlu diubah** — cukup tulis skemanya.
4. Wajib tersedia 5 template: `home.js`, `post.js`, `page.js`, `archive.js`, `not-found.js`. Masing-masing adalah fungsi murni `(ctx) => string HTML`.
5. Aktifkan lewat menu **Tema** (galeri), lalu atur lewat menu **Sesuaikan** — tanpa menyentuh `config.json` secara manual.

**Objek `ctx`** yang diterima setiap template berisi:

| Field | Isi |
|---|---|
| `config` | seluruh `config.json` |
| `U` | helper URL: `url()`, `abs()`, `baseUrl`, `basePath` |
| `lib` | helper murni: `esc`, `attr`, `slugify`, `formatDate` |
| `site` | `widgets`, `recentPosts`, `categoryNames`, `tagNames` |
| `seo` | `title`, `description`, `canonical`, `ogType`, `ogImage`, `jsonLd[]` |
| `themeVars` | peta CSS variable dari `themeOptions` |
| *(per halaman)* | `posts`/`pageNum`/`totalPages` (home), `post`/`related` (post), `page` (page), `kind`/`term`/`posts` (archive) |

Partial `head.js` sudah merender seluruh meta/Open Graph/JSON-LD dari `ctx.seo`, jadi **tema baru otomatis SEO-ready** tanpa menulis ulang logika meta.

---

## 🔍 Fitur SEO Bawaan

Setiap halaman artikel otomatis menghasilkan:

- `<title>` dan `<meta name="description">` unik
- `<link rel="canonical">` untuk mencegah duplikat
- Open Graph (`og:title`, `og:description`, `og:image`, `og:type=article`)
- Twitter Card
- JSON-LD **BlogPosting** + **BreadcrumbList**
- Estimasi waktu baca

Situs juga menghasilkan `sitemap.xml`, `rss.xml`, dan `robots.txt`.

---

## ❓ Troubleshooting

| Masalah | Solusi |
|---|---|
| CSS/gambar tidak muncul | Pastikan `basePath` di `config.json` benar (mis. `/blog-cms`) |
| Halaman 404 setelah deploy | Tunggu workflow Actions selesai; cek Source = GitHub Actions |
| Link antar-halaman rusak | Periksa `basePath` — kosongkan untuk user-site/domain sendiri |
| "Token tidak valid" | Cek permission **Contents: Read and write** & masa berlaku token |
| Artikel tak muncul di blog | Pastikan `status: published`, lalu tunggu build selesai |
| Workflow Actions gagal | Buka tab Actions → klik run yang gagal untuk lihat log |
| Upload media gagal / gambar tidak masuk repo | Pastikan konfigurasi owner, repository, dan branch benar. Token GitHub harus punya permission **Contents: Read and write** pada repository tersebut. |
| Tombol upload media tidak membuka pilihan file | Gunakan versi terbaru CMS ini; input file sudah dibuat kompatibel untuk browser desktop dan mobile. |

---

## 🛠️ Pengembangan Lanjutan

- Tambah halaman statis baru di `content/pages/`
- Integrasi komentar (Giscus / Utterances berbasis GitHub Issues)
- Login multi-user via proxy OAuth (Cloudflare Worker)
- Sinkronisasi konten ke WordPress via REST API
- Tambah fitur pencarian sisi-klien (mis. dengan index JSON)

---

Dibuat untuk Anda yang ingin blog cepat, gratis, dan sepenuhnya dimiliki sendiri. Selamat berkarya! 🚀
