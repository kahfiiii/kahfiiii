# Setup Guide — Snake Contribution Graph

## Langkah-langkah

### 1. Buat Special Profile Repository
GitHub profile README harus berada di repository dengan nama yang sama persis dengan username kamu.

- Buka GitHub -> New Repository
- Nama repo: `kahfiiii` (sama persis dengan username)
- Centang: **Public** dan **Add a README file**
- Klik Create repository

---

### 2. Upload file-file ini ke repo tersebut

Struktur folder yang harus ada di repo `kahfiiii/kahfiiii`:

```
kahfiiii/              <-- root repo
├── README.md
└── .github/
    └── workflows/
        └── snake.yml
```

---

### 3. Aktifkan GitHub Actions Permissions

Pergi ke repo -> **Settings** -> **Actions** -> **General**

Scroll ke bawah ke bagian **Workflow permissions**, pilih:
- [x] Read and write permissions
- [x] Allow GitHub Actions to create and approve pull requests

Klik **Save**.

---

### 4. Jalankan workflow pertama kali (manual)

- Pergi ke tab **Actions** di repo kamu
- Klik workflow **"Generate Snake Animation"**
- Klik tombol **"Run workflow"** -> **Run workflow**
- Tunggu ~1-2 menit sampai selesai

Setelah berhasil, branch baru bernama `output` akan muncul, berisi file `snake.svg` dan `snake-dark.svg`.

---

### 5. Verifikasi URL snake

Cek apakah file sudah ada di:
```
https://raw.githubusercontent.com/kahfiiii/kahfiiii/output/snake.svg
https://raw.githubusercontent.com/kahfiiii/kahfiiii/output/snake-dark.svg
```

Kalau sudah muncul, README kamu langsung tampil dengan animasi snake.

---

### 6. Otomatis update setiap hari

Workflow sudah di-set `cron: "0 0 * * *"` — snake akan update otomatis setiap tengah malam UTC, memakan contribution baru kamu.

---

## Troubleshooting

| Masalah | Solusi |
|---|---|
| Workflow gagal dengan error permission | Pastikan Write permissions sudah aktif di Settings -> Actions |
| Branch `output` tidak muncul | Coba jalankan workflow manual sekali lagi |
| SVG tidak muncul di README | Tunggu beberapa menit, GitHub cache gambar ~5 menit |
| Snake tidak bergerak | Pastikan menggunakan `<picture>` tag, bukan `![img]()` biasa |

---

## Cara kerja

1. Workflow jalan setiap hari
2. `Platane/snk` action fetch data contribution kamu dari GitHub API
3. Menghasilkan SVG animasi dengan snake yang memakan contribution cells
4. File di-push ke branch `output`
5. README load SVG langsung dari branch `output`
