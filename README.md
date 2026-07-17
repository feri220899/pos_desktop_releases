<div align="center">

<img src="https://img.shields.io/badge/POS-Desktop-4f46e5?style=for-the-badge&logo=shopify&logoColor=white" alt="POS Desktop" height="40" />

# 🏪 POS Desktop

**Aplikasi Point of Sale (Kasir) modern, cepat, dan _offline-first_ untuk toko ritel Indonesia.**

Jualan tetap jalan walau internet mati. Kelola produk, stok, konsinyasi, laporan, hingga banyak cabang & gudang pusat — dari satu aplikasi.

<br />

[![Rilis Terbaru](https://img.shields.io/github/v/release/feri220899/pos_desktop_releases?style=for-the-badge&label=Versi&color=4f46e5)](https://github.com/feri220899/pos_desktop_releases/releases/latest)
[![Total Unduhan](https://img.shields.io/github/downloads/feri220899/pos_desktop_releases/total?style=for-the-badge&label=Unduhan&color=10b981)](https://github.com/feri220899/pos_desktop_releases/releases/latest)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-0ea5e9?style=for-the-badge)](#-instalasi)

<br />

### ⬇️ Unduh Sekarang

[![Download](https://img.shields.io/badge/⬇%20DOWNLOAD-Rilis%20Terbaru-4f46e5?style=for-the-badge&logoColor=white)](https://github.com/feri220899/pos_desktop_releases/releases/latest)

<sub>Pilih installer sesuai sistem operasi Anda di halaman rilis</sub>

<table>
<tr>
<td align="center">

**🪟 Windows**

Installer `.exe` (NSIS)

</td>
<td align="center">

**🐧 Linux**

`.AppImage` &amp; `.deb`

</td>
</tr>
</table>

</div>

---

## ✨ Fitur Unggulan

| | Fitur | Keterangan |
|---|---|---|
| 🧾 | **Kasir Cepat** | Scan barcode, cari produk, multi-satuan (PCS/BOX/KG), hitung kembalian, cetak struk otomatis |
| 📦 | **Manajemen Produk** | Multi-satuan & konversi, multi-barcode, histori harga, kategori & pemasok, soft-delete + pulihkan |
| 📊 | **Stok & Opname** | Pantau stok real-time, riwayat pergerakan, koreksi, sesi stok opname (input fisik massal → penyesuaian) |
| 🤝 | **Konsinyasi** | Rekap produk titipan per pemasok/produk, saldo hak pemasok, catat setoran |
| 📈 | **Laporan & Dashboard** | KPI harian (omzet/laba/transaksi), grafik 7 hari, produk terlaris, stok kritis, laba kotor tersnapshot |
| 🖨️ | **Cetak Struk** | Silent print ke printer thermal (80mm/58mm), auto-print, atau dialog cetak |
| 🏢 | **Multi-Cabang & Gudang Pusat** | Kelola banyak cabang, transfer stok gudang→cabang, permintaan stok, katalog produk pusat |
| 🌐 | **Master–Client LAN** | Satu master jalankan server lokal, beberapa client kasir terhubung via jaringan (mDNS) |
| 👥 | **Multi-User & Hak Akses** | Role & permission (admin, kasir, dll) — batasi akses per modul |
| 🔒 | **Offline-First** | Database lokal SQLite — semua transaksi tetap tersimpan tanpa internet |

---

## 🚀 Instalasi

1. Buka **[halaman rilis terbaru »](https://github.com/feri220899/pos_desktop_releases/releases/latest)**
2. Unduh berkas sesuai OS Anda:
   - **Windows** → `POS-Desktop-Setup-x.x.x.exe`
   - **Linux** → `POS-Desktop-x.x.x.AppImage` atau `pos-desktop_x.x.x_amd64.deb`
3. Jalankan installer, lalu buka aplikasi.
4. Saat pertama kali dibuka, lakukan **aktivasi lisensi** dan pilih **mode** (Master / Client).

> 💡 **Linux AppImage:** beri izin eksekusi dulu — `chmod +x POS-Desktop-*.AppImage`, lalu klik dua kali.

---

## 🖼️ Tampilan

> _Tambahkan tangkapan layar aplikasi di sini (Dashboard, Kasir, Produk, Laporan)._

<!--
![Dashboard](docs/screenshots/dashboard.png)
![Kasir](docs/screenshots/kasir.png)
-->

---

## 🧱 Teknologi

- **[Electron](https://www.electronjs.org/)** — kerangka aplikasi desktop lintas platform
- **[Vue 3](https://vuejs.org/)** + **Vue Router** + **Pinia** — antarmuka reaktif
- **[TailwindCSS 4](https://tailwindcss.com/)** + **DaisyUI** — desain UI
- **[better-sqlite3](https://github.com/WiseLibs/better-sqlite3)** — database lokal cepat
- **Express** — server backend tertanam (mode master)
- **electron-vite** + **electron-builder** — build & packaging

---

## 🏗️ Arsitektur Singkat

```
┌─────────────────────────────┐        ┌──────────────────────────────┐
│  MODE MASTER                 │  LAN   │  MODE CLIENT                  │
│  • Express server (:3001)    │◀──────▶│  • Terhubung ke IP master     │
│  • SQLite lokal (offline)    │  mDNS  │  • Antarmuka kasir            │
│  • Antarmuka kasir + admin   │        │                               │
└─────────────────────────────┘        └──────────────────────────────┘
              │
              ▼ (online, opsional)
      Server Lisensi & Gudang Pusat (Laravel)
      — aktivasi lisensi, transfer stok antar cabang
```

- **Offline-first:** kasir & seluruh data toko tersimpan di SQLite lokal — tidak butuh internet untuk berjualan.
- **Sinkronisasi cabang:** terima transfer stok dari gudang pusat & ajukan permintaan stok saat online.

---

## 👨‍💻 Build dari Sumber (untuk Pengembang)

```bash
# Prasyarat: Node.js 18+ dan npm

npm install          # pasang dependency

npm run dev          # jalankan mode pengembangan (hot reload)
npm run build        # build bundle produksi
npm run dist         # build + buat installer (AppImage/deb di Linux, NSIS di Windows)
```

Struktur ringkas:

```
src/
  main/       # Electron main process (window, IPC, service: lisensi, printer, discovery)
  preload/    # jembatan aman renderer ↔ main
  backend/    # Express + SQLite (controllers, models, migrations)
  renderer/   # Aplikasi Vue 3 (views, components, stores)
```

---

## 📄 Lisensi & Aktivasi

Aplikasi ini memerlukan **kunci lisensi** untuk aktivasi. Lisensi terikat pada perangkat
(berdasarkan identitas perangkat unik) dan divalidasi ke server lisensi.
Hubungi penyedia untuk memperoleh kunci lisensi.

---

<div align="center">

Dibuat dengan ❤️ oleh **Feri Jumaidi**

⭐ Beri bintang jika aplikasi ini bermanfaat!

[⬇️ Unduh Rilis Terbaru](https://github.com/feri220899/pos_desktop_releases/releases/latest)

</div>
