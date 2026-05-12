# 📋 PRD — Product Requirements Document

# FinTrack: Invoice & Expense Tracker

---

## Informasi Dokumen

| Field              | Detail                                |
| ------------------ | ------------------------------------- |
| **Nama Produk**    | Expense Tracker                       |
| **Versi**          | 1.0.0                                 |
| **Tanggal Dibuat** | 2026                                  |
| **Author**         | [Rizky Wahyudi]                       |
| **Status**         | Draft                                 |
| **Platform**       | Web App (Desktop & Mobile Responsive) |

---

## 1. 🎯 Overview

### 1.1 Latar Belakang

Freelancer dan pemilik UMKM sering menghadapi masalah dalam mengelola keuangan bisnis mereka sehari-hari. Invoice kepada klien tidak terpantau statusnya, pengeluaran operasional tidak tercatat dengan rapi, dan tidak ada laporan keuangan yang bisa dijadikan acuan bisnis.

### 1.2 Problem Statement

> Freelancer dan UMKM kesulitan mencatat keuangan bisnis secara terstruktur — invoice ke klien tidak terpantau, pengeluaran tidak tercatat, dan tidak ada laporan keuangan yang jelas sebagai dasar pengambilan keputusan bisnis.

### 1.3 Solusi

Membangun aplikasi web **FinTrack** yang membantu freelancer dan UMKM untuk:

- Membuat dan mengelola invoice kepada klien
- Mencatat dan mengkategorikan pengeluaran bisnis
- Memantau status pembayaran invoice secara real-time
- Melihat laporan keuangan bisnis secara ringkas dan jelas

### 1.4 Target Pengguna

- Freelancer (desainer, developer, konsultan, fotografer, dll.)
- Pemilik UMKM (usaha kecil & menengah)
- Konsultan independen

---

## 2. 👥 User Roles

### 2.1 Admin

- Mengelola seluruh data pengguna aplikasi
- Melihat statistik penggunaan aplikasi
- Memiliki akses penuh ke semua fitur

### 2.2 User (Freelancer / Pemilik UMKM)

- Mengelola data klien milik sendiri
- Membuat dan mengelola invoice
- Mencatat pengeluaran bisnis
- Melihat laporan keuangan pribadi

> **Catatan:** Setiap user hanya bisa mengakses data miliknya sendiri. Data antar user sepenuhnya terisolasi.

---

## 3. ✅ Functional Requirements

### 3.1 Module: Authentication (AUTH)

| ID      | Fitur          | Deskripsi                                                      | Priority       |
| ------- | -------------- | -------------------------------------------------------------- | -------------- |
| AUTH-01 | Register       | User bisa mendaftar akun baru dengan nama, email, dan password | 🔴 Must Have   |
| AUTH-02 | Login          | User bisa login menggunakan email & password                   | 🔴 Must Have   |
| AUTH-03 | Logout         | User bisa keluar dari sesi aktif                               | 🔴 Must Have   |
| AUTH-04 | Reset Password | User bisa reset password melalui link yang dikirim ke email    | 🟡 Should Have |
| AUTH-05 | Edit Profil    | User bisa mengubah nama, foto profil, dan password             | 🟡 Should Have |

### 3.2 Module: Dashboard (DASH)

| ID      | Fitur               | Deskripsi                                                       | Priority       |
| ------- | ------------------- | --------------------------------------------------------------- | -------------- |
| DASH-01 | Total Pemasukan     | Menampilkan total invoice yang sudah dibayar bulan ini          | 🔴 Must Have   |
| DASH-02 | Total Pengeluaran   | Menampilkan total pengeluaran yang tercatat bulan ini           | 🔴 Must Have   |
| DASH-03 | Invoice Outstanding | Daftar invoice yang belum dibayar atau sudah overdue            | 🔴 Must Have   |
| DASH-04 | Grafik Keuangan     | Grafik bar/line perbandingan pemasukan vs pengeluaran per bulan | 🟡 Should Have |
| DASH-05 | Invoice Terbaru     | Widget menampilkan 5 invoice terakhir yang dibuat               | 🟡 Should Have |

### 3.3 Module: Client Management (CLT)

| ID     | Fitur        | Deskripsi                                                  | Priority       |
| ------ | ------------ | ---------------------------------------------------------- | -------------- |
| CLT-01 | Tambah Klien | Menambahkan data klien baru (nama, email, telepon, alamat) | 🔴 Must Have   |
| CLT-02 | Edit Klien   | Mengubah data klien yang sudah ada                         | 🔴 Must Have   |
| CLT-03 | Hapus Klien  | Menghapus data klien (soft delete)                         | 🔴 Must Have   |
| CLT-04 | Detail Klien | Melihat profil klien beserta riwayat semua invoice         | 🔴 Must Have   |
| CLT-05 | Search Klien | Mencari klien berdasarkan nama atau email                  | 🟡 Should Have |

### 3.4 Module: Invoice Management (INV)

| ID     | Fitur           | Deskripsi                                                       | Priority        |
| ------ | --------------- | --------------------------------------------------------------- | --------------- |
| INV-01 | Buat Invoice    | Membuat invoice baru dengan pilih klien & tambah item pekerjaan | 🔴 Must Have    |
| INV-02 | Edit Invoice    | Mengubah invoice (hanya boleh jika status masih Draft)          | 🔴 Must Have    |
| INV-03 | Hapus Invoice   | Menghapus invoice (hanya boleh jika status masih Draft)         | 🔴 Must Have    |
| INV-04 | Nomor Otomatis  | Generate nomor invoice otomatis, contoh: INV-2025-001           | 🔴 Must Have    |
| INV-05 | Ubah Status     | Mengubah status invoice: Draft → Sent → Paid                    | 🔴 Must Have    |
| INV-06 | Due Date        | Menentukan batas waktu pembayaran invoice                       | 🔴 Must Have    |
| INV-07 | Auto Overdue    | Status otomatis berubah menjadi Overdue jika due date terlewat  | 🔴 Must Have    |
| INV-08 | Download PDF    | Generate dan download invoice dalam format PDF                  | 🟡 Should Have  |
| INV-09 | Kirim Email     | Mengirim invoice ke email klien langsung dari aplikasi          | 🟢 Nice to Have |
| INV-10 | Tambah PPN      | Opsi untuk menambahkan pajak PPN (11%) ke total invoice         | 🟢 Nice to Have |
| INV-11 | Catatan Invoice | Kolom catatan/notes tambahan untuk klien                        | 🟡 Should Have  |

### 3.5 Module: Expense Tracker (EXP)

| ID     | Fitur              | Deskripsi                                                        | Priority       |
| ------ | ------------------ | ---------------------------------------------------------------- | -------------- |
| EXP-01 | Tambah Pengeluaran | Mencatat pengeluaran baru dengan nominal, tanggal, dan deskripsi | 🔴 Must Have   |
| EXP-02 | Edit Pengeluaran   | Mengubah data pengeluaran yang sudah tercatat                    | 🔴 Must Have   |
| EXP-03 | Hapus Pengeluaran  | Menghapus catatan pengeluaran                                    | 🔴 Must Have   |
| EXP-04 | Kategori           | Pengeluaran bisa dikategorikan (Operasional, Marketing, dll.)    | 🔴 Must Have   |
| EXP-05 | Upload Bukti       | Upload foto atau PDF sebagai bukti transaksi                     | 🟡 Should Have |
| EXP-06 | Filter             | Filter daftar pengeluaran berdasarkan tanggal dan kategori       | 🟡 Should Have |

### 3.6 Module: Laporan / Reports (RPT)

| ID     | Fitur           | Deskripsi                                                           | Priority        |
| ------ | --------------- | ------------------------------------------------------------------- | --------------- |
| RPT-01 | Laporan Bulanan | Ringkasan pemasukan dan pengeluaran per bulan yang dipilih          | 🔴 Must Have    |
| RPT-02 | Rekap Invoice   | Rekapitulasi jumlah invoice per status (Draft, Sent, Paid, Overdue) | 🔴 Must Have    |
| RPT-03 | Export PDF      | Download laporan keuangan dalam format PDF                          | 🟡 Should Have  |
| RPT-04 | Export Excel    | Download data dalam format Excel (.xlsx)                            | 🟢 Nice to Have |

---

## 4. 🚫 Non-Functional Requirements

| Aspek             | Ketentuan                                                                    |
| ----------------- | ---------------------------------------------------------------------------- |
| **Security**      | Autentikasi via Laravel Sanctum; data user terisolasi per akun               |
| **Validasi**      | Semua form input divalidasi di sisi backend menggunakan Laravel Form Request |
| **Responsive**    | Tampilan mobile-friendly menggunakan utility class Tailwind CSS              |
| **Performance**   | Target waktu load halaman di bawah 3 detik                                   |
| **Authorization** | Akses resource dikontrol via Laravel Policy                                  |

---

## 5. 📌 Invoice Status Flow

```
[DRAFT] ──► [SENT] ──► [PAID]
   │
   └─────────────────► [OVERDUE]  ← otomatis jika due date sudah terlewat
```

| Status  | Keterangan                          | Bisa Diedit? | Bisa Dihapus? |
| ------- | ----------------------------------- | ------------ | ------------- |
| Draft   | Invoice baru dibuat, belum dikirim  | ✅ Ya        | ✅ Ya         |
| Sent    | Invoice sudah dikirim ke klien      | ❌ Tidak     | ❌ Tidak      |
| Paid    | Invoice sudah dibayar oleh klien    | ❌ Tidak     | ❌ Tidak      |
| Overdue | Melewati due date dan belum dibayar | ❌ Tidak     | ❌ Tidak      |

---

## 6. 🗓️ Scope V1.0

### ✅ In Scope (Yang dikerjakan sekarang)

- Semua fitur dengan prioritas **Must Have** (🔴)
- Generate PDF untuk invoice
- Dashboard dengan grafik keuangan sederhana
- Laporan keuangan bulanan
- Sistem autentikasi dengan data isolation per user

### ❌ Out of Scope (Pengembangan selanjutnya)

- Integrasi payment gateway (Midtrans, Xendit, dll.)
- Multi-currency support
- Versi mobile app (Android/iOS)
- Multi-bisnis dalam satu akun
- Integrasi software akuntansi (Jurnal, Accurate, dll.)
- Fitur subscription / recurring invoice

---

## 7. 🛠️ Tech Stack

| Layer             | Teknologi                        |
| ----------------- | -------------------------------- |
| Backend Framework | Laravel 11                       |
| Authentication    | Laravel Sanctum                  |
| Frontend Styling  | Tailwind CSS / Bootstrap / KT-UI |
| Database          | MySQL                            |
| PDF Generation    | DomPDF (barryvdh/laravel-dompdf) |
| File Storage      | Laravel Storage (local / S3)     |
| Charts            | Chart.js / ApexCharts            |

---

_Dokumen ini bersifat living document dan akan diperbarui seiring perkembangan project._
