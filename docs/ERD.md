# 🗃️ ERD — Entity Relationship Document

# FinTrack: Invoice & Expense Tracker

---

## 1. Daftar Tabel & Kolom

### 📋 Tabel: `users`

> Menyimpan data akun pengguna aplikasi.

| Kolom               | Tipe Data            | Keterangan                  |
| ------------------- | -------------------- | --------------------------- |
| `id`                | BIGINT UNSIGNED      | Primary Key, Auto Increment |
| `name`              | VARCHAR(100)         | Nama lengkap user           |
| `email`             | VARCHAR(100)         | Email user, harus unik      |
| `email_verified_at` | TIMESTAMP            | Waktu verifikasi email      |
| `password`          | VARCHAR(255)         | Password (hashed bcrypt)    |
| `avatar`            | VARCHAR(255)         | Path foto profil (nullable) |
| `role`              | ENUM('admin','user') | Role user, default: 'user'  |
| `remember_token`    | VARCHAR(100)         | Token untuk "remember me"   |
| `created_at`        | TIMESTAMP            | Waktu akun dibuat           |
| `updated_at`        | TIMESTAMP            | Waktu akun terakhir diubah  |

---

### 📋 Tabel: `clients`

> Menyimpan data klien milik setiap user.

| Kolom        | Tipe Data       | Keterangan                                |
| ------------ | --------------- | ----------------------------------------- |
| `id`         | BIGINT UNSIGNED | Primary Key, Auto Increment               |
| `user_id`    | BIGINT UNSIGNED | Foreign Key → users.id                    |
| `name`       | VARCHAR(100)    | Nama klien atau nama perusahaan           |
| `email`      | VARCHAR(100)    | Email klien (nullable)                    |
| `phone`      | VARCHAR(20)     | Nomor telepon klien (nullable)            |
| `address`    | TEXT            | Alamat lengkap klien (nullable)           |
| `notes`      | TEXT            | Catatan tambahan tentang klien (nullable) |
| `deleted_at` | TIMESTAMP       | Soft delete timestamp (nullable)          |
| `created_at` | TIMESTAMP       | Waktu data dibuat                         |
| `updated_at` | TIMESTAMP       | Waktu data terakhir diubah                |

---

### 📋 Tabel: `invoices`

> Menyimpan header data invoice.

| Kolom            | Tipe Data                             | Keterangan                              |
| ---------------- | ------------------------------------- | --------------------------------------- |
| `id`             | BIGINT UNSIGNED                       | Primary Key, Auto Increment             |
| `user_id`        | BIGINT UNSIGNED                       | Foreign Key → users.id                  |
| `client_id`      | BIGINT UNSIGNED                       | Foreign Key → clients.id                |
| `invoice_number` | VARCHAR(30)                           | Nomor invoice unik, cth: INV-2025-001   |
| `status`         | ENUM('draft','sent','paid','overdue') | Status invoice, default: 'draft'        |
| `issue_date`     | DATE                                  | Tanggal invoice dibuat                  |
| `due_date`       | DATE                                  | Batas waktu pembayaran                  |
| `subtotal`       | DECIMAL(15,2)                         | Total sebelum pajak                     |
| `tax_percent`    | DECIMAL(5,2)                          | Persentase pajak, cth: 11.00 (nullable) |
| `tax_amount`     | DECIMAL(15,2)                         | Nominal pajak (nullable)                |
| `total`          | DECIMAL(15,2)                         | Total akhir setelah pajak               |
| `notes`          | TEXT                                  | Catatan tambahan untuk klien (nullable) |
| `paid_at`        | TIMESTAMP                             | Waktu invoice ditandai lunas (nullable) |
| `deleted_at`     | TIMESTAMP                             | Soft delete timestamp (nullable)        |
| `created_at`     | TIMESTAMP                             | Waktu data dibuat                       |
| `updated_at`     | TIMESTAMP                             | Waktu data terakhir diubah              |

---

### 📋 Tabel: `invoice_items`

> Menyimpan detail item pekerjaan dalam sebuah invoice.

| Kolom         | Tipe Data       | Keterangan                    |
| ------------- | --------------- | ----------------------------- |
| `id`          | BIGINT UNSIGNED | Primary Key, Auto Increment   |
| `invoice_id`  | BIGINT UNSIGNED | Foreign Key → invoices.id     |
| `description` | VARCHAR(255)    | Deskripsi pekerjaan / item    |
| `quantity`    | DECIMAL(10,2)   | Jumlah / kuantitas            |
| `unit_price`  | DECIMAL(15,2)   | Harga per satuan              |
| `amount`      | DECIMAL(15,2)   | Total = quantity × unit_price |
| `created_at`  | TIMESTAMP       | Waktu data dibuat             |
| `updated_at`  | TIMESTAMP       | Waktu data terakhir diubah    |

---

### 📋 Tabel: `expense_categories`

> Menyimpan kategori pengeluaran milik setiap user.

| Kolom        | Tipe Data       | Keterangan                                 |
| ------------ | --------------- | ------------------------------------------ |
| `id`         | BIGINT UNSIGNED | Primary Key, Auto Increment                |
| `user_id`    | BIGINT UNSIGNED | Foreign Key → users.id                     |
| `name`       | VARCHAR(100)    | Nama kategori, cth: Operasional, Marketing |
| `color`      | VARCHAR(7)      | Warna hex untuk tampilan UI (nullable)     |
| `created_at` | TIMESTAMP       | Waktu data dibuat                          |
| `updated_at` | TIMESTAMP       | Waktu data terakhir diubah                 |

---

### 📋 Tabel: `expenses`

> Menyimpan catatan pengeluaran bisnis setiap user.

| Kolom                 | Tipe Data       | Keterangan                              |
| --------------------- | --------------- | --------------------------------------- |
| `id`                  | BIGINT UNSIGNED | Primary Key, Auto Increment             |
| `user_id`             | BIGINT UNSIGNED | Foreign Key → users.id                  |
| `expense_category_id` | BIGINT UNSIGNED | Foreign Key → expense_categories.id     |
| `title`               | VARCHAR(150)    | Judul / nama pengeluaran                |
| `amount`              | DECIMAL(15,2)   | Nominal pengeluaran                     |
| `date`                | DATE            | Tanggal pengeluaran terjadi             |
| `description`         | TEXT            | Deskripsi detail pengeluaran (nullable) |
| `receipt_path`        | VARCHAR(255)    | Path file bukti transaksi (nullable)    |
| `deleted_at`          | TIMESTAMP       | Soft delete timestamp (nullable)        |
| `created_at`          | TIMESTAMP       | Waktu data dibuat                       |
| `updated_at`          | TIMESTAMP       | Waktu data terakhir diubah              |

---

### 📋 Tabel: `personal_access_tokens`

> Dikelola otomatis oleh Laravel Sanctum untuk API authentication.

| Kolom            | Tipe Data       | Keterangan                                |
| ---------------- | --------------- | ----------------------------------------- |
| `id`             | BIGINT UNSIGNED | Primary Key, Auto Increment               |
| `tokenable_type` | VARCHAR(255)    | Polymorphic model type                    |
| `tokenable_id`   | BIGINT UNSIGNED | Polymorphic model id                      |
| `name`           | VARCHAR(255)    | Nama token                                |
| `token`          | VARCHAR(64)     | Hash token, harus unik                    |
| `abilities`      | TEXT            | Kemampuan token (nullable)                |
| `last_used_at`   | TIMESTAMP       | Waktu token terakhir digunakan (nullable) |
| `expires_at`     | TIMESTAMP       | Waktu expired token (nullable)            |
| `created_at`     | TIMESTAMP       | Waktu data dibuat                         |
| `updated_at`     | TIMESTAMP       | Waktu data terakhir diubah                |

---

## 2. Relasi Antar Tabel

```
users
 │
 ├──< clients              (1 user memiliki banyak klien)
 │      └──< invoices      (1 klien memiliki banyak invoice)
 │              └──< invoice_items  (1 invoice memiliki banyak item)
 │
 ├──< invoices             (1 user memiliki banyak invoice)
 │
 ├──< expense_categories   (1 user memiliki banyak kategori pengeluaran)
 │      └──< expenses      (1 kategori memiliki banyak pengeluaran)
 │
 └──< expenses             (1 user memiliki banyak pengeluaran)
```

---

## 3. Diagram ERD (Text Format)

```
┌─────────────────────┐         ┌────────────────────────┐
│        users        │         │        clients         │
├─────────────────────┤         ├────────────────────────┤
│ PK  id              │──┐  ┌──>│ PK  id                 │
│     name            │  │  │   │ FK  user_id            │
│     email           │  │  │   │     name               │
│     password        │  │  │   │     email              │
│     role            │  │  │   │     phone              │
│     avatar          │  └──┘   │     address            │
└─────────────────────┘         │     deleted_at         │
         │                      └────────────┬───────────┘
         │                                   │
         │                                   │ 1 klien punya banyak invoice
         │                                   ▼
         │                      ┌────────────────────────┐       ┌─────────────────────┐
         │                      │       invoices         │       │    invoice_items    │
         │                      ├────────────────────────┤       ├─────────────────────┤
         │                      │ PK  id                 │──────>│ PK  id              │
         └─────────────────────>│ FK  user_id            │       │ FK  invoice_id      │
                                │ FK  client_id          │       │     description     │
                                │     invoice_number     │       │     quantity        │
                                │     status             │       │     unit_price      │
                                │     issue_date         │       │     amount          │
                                │     due_date           │       └─────────────────────┘
                                │     subtotal           │
                                │     tax_percent        │
                                │     total              │
                                │     paid_at            │
                                │     deleted_at         │
                                └────────────────────────┘

┌─────────────────────┐         ┌────────────────────────┐
│  expense_categories │         │        expenses        │
├─────────────────────┤         ├────────────────────────┤
│ PK  id              │──────┐  │ PK  id                 │
│ FK  user_id         │      └─>│ FK  expense_category_id│
│     name            │         │ FK  user_id            │
│     color           │         │     title              │
└─────────────────────┘         │     amount             │
                                │     date               │
                                │     description        │
                                │     receipt_path       │
                                │     deleted_at         │
                                └────────────────────────┘
```

---

## 4. Catatan Penting

- **Soft Delete** digunakan pada tabel `clients`, `invoices`, dan `expenses` agar data tidak hilang permanen.
- **Nomor Invoice** (`invoice_number`) di-generate otomatis dengan format `INV-YYYY-NNN` (contoh: `INV-2025-001`).
- **Status Overdue** diperbarui secara otomatis melalui Laravel Scheduled Command yang berjalan setiap hari.
- **Data Isolation** dijamin karena setiap query selalu difilter berdasarkan `user_id` dari user yang sedang login.
- **receipt_path** menyimpan path file relatif di storage Laravel, bukan URL absolut.
