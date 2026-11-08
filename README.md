# 🏭 Equipment Auction Platform — CV ANUGERAH KEMBAR MAKMUR JAYA

Platform lelang mesin dan peralatan industri berbasis web (frontend prototype) yang dirancang untuk **CV ANUGERAH KEMBAR MAKMUR JAYA (CV AKMJ)**. Aplikasi ini mendukung lelang hybrid (online & offline) dengan sistem **Guest Bidding** tanpa registrasi akun — cukup verifikasi OTP simulasi via WhatsApp.

> ⚠️ **Status:** Frontend Prototype / Simulasi — data disimpan di `localStorage` browser, bukan backend production.

---

## 🚀 Fitur Utama

### Portal Publik
| Fitur | Deskripsi |
|-------|-----------|
| **Beranda** | Hero section, lelang aktif, jadwal mendatang, hasil terbaru, panduan "Cara Kerja", FAQ |
| **Katalog Lelang** | Grid produk dengan filter kategori, status, dan pencarian real-time |
| **Detail Barang** | Spesifikasi lengkap, riwayat penawaran (nama disamarkan), countdown timer, tombol bid |
| **Guest Bidding** | Alur 3 langkah: Identitas → OTP WhatsApp simulasi → Pengajuan nominal |
| **Jadwal Lelang** | Daftar agenda lelang aktif/mendatang/selesai |
| **Hasil Lelang** | Tabel arsip pemenang, harga akhir, dan status pembayaran |
| **Tentang Kami** | Profil perusahaan, visi mekanisme, lokasi kantor |

### Admin Dashboard
| Modul | Fungsi |
|-------|--------|
| **Overview** | Statistik total barang, lelang aktif, total bid, peserta + grafik Chart.js |
| **Data Barang** | CRUD barang lelang (tambah, ubah status, hapus) |
| **Input Bid Offline** | Input penawaran peserta di lokasi fisik (auction hall) |
| **Monitoring** | Audit trail semua bid dengan label `ONLINE` / `OFFLINE` |
| **Peserta** | Daftar peserta terverifikasi OTP |
| **Pembayaran** | Kelola status pelunasan pemenang lelang |

---

## 🛠️ Teknologi

- **HTML5** — struktur semantik
- **Tailwind CSS** (via CDN) — styling utility-first, custom config (`navy`, `brand`, animasi)
- **Chart.js** (via CDN) — visualisasi aktivitas bidding di admin
- **Font Awesome 6.4** — ikon
- **Google Fonts** — Inter & Plus Jakarta Sans
- **Vanilla JavaScript** — logika state, DOM rendering, `localStorage` persistence

Tidak diperlukan build tools / `npm install`. Cukup buka file HTML di browser.

---

## 📁 Struktur Data

Data disimpan di `localStorage` dengan dua key utama:

```js
// Key: 'akmj_auction_items'
[
  {
    id: 'item-1',
    title: 'Industrial Refrigeration Compressor Bitzer 50HP',
    category: 'Refrigeration',
    location: 'Gudang CV AKMJ Cikarang, Jawa Barat',
    startPrice: 45000000,
    currentBid: 52000000,
    minIncrement: 1000000,
    status: 'ACTIVE' | 'UPCOMING' | 'ENDED',
    endTime: 1712345678901,
    image: 'https://...',
    description: '...',
    specifications: '...',
    condition: '...',
    bidCount: 4,
    bids: [
      { id, name, amount, time, source: 'ONLINE'|'OFFLINE' }
    ],
    winner: { name, amount, phone } | null,
    paymentStatus: 'PAID' | 'UNPAID'
  }
]

// Key: 'akmj_auction_participants'
[ { name, phone, email, verifiedAt } ]
