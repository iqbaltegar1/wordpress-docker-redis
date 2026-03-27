# 🚀 Dockerize WordPress dengan MySQL dan Redis

## 📌 Deskripsi

Project ini merupakan implementasi **WordPress CMS menggunakan Docker Compose** dengan:

- 🐘 MySQL sebagai database
- ⚡ Redis sebagai object cache

Tujuan project ini adalah untuk memahami konsep **multi-container orchestration**, **networking antar container**, serta **data persistence menggunakan volume**.

---

## 🎯 Learning Objectives

- Memahami multi-container setup dengan Docker Compose
- Konfigurasi service dependencies (`depends_on`)
- Docker networking antar container
- Volume untuk data persistence
- Environment variables configuration

---

## 🧱 Arsitektur Sistem

```
[ Browser ]
     ↓
[ WordPress Container ]
     ↓
 ┌───────────────┐
 ↓               ↓
[ MySQL ]     [ Redis ]
(Database)    (Cache)
```

---

## 📂 Struktur Project

```
wordpress-docker/
│
├── docker-compose.yml
├── README.md
```

---

## ⚙️ Konfigurasi Docker Compose

Project ini terdiri dari 3 service:

### 1. WordPress

- Image: `wordpress:latest`
- Port: `8000:80`
- Terhubung ke MySQL dan Redis

### 2. MySQL

- Image: `mysql:5.7`
- Menyimpan database WordPress

### 3. Redis

- Image: `redis:alpine`
- Digunakan untuk object caching

---

## ▶️ Cara Menjalankan Project

### 1. Clone repository

```bash
git clone <repository-url>
cd wordpress-docker
```

### 2. Jalankan Docker Compose

```bash
docker-compose up -d
```

### 3. Akses WordPress

Buka browser:

```
http://localhost:8000
```

---

## 🧪 Testing & Verifikasi

### ✅ 1. WordPress berjalan

- Bisa diakses di browser
- Bisa login ke dashboard

---

### ✅ 2. MySQL Connection

- Bisa membuat post / page
- Tidak ada error database

---

### ✅ 3. Redis Connection

#### Cek Redis via CLI:

```bash
docker exec -it wordpress-docker-redis-1 redis-cli ping
```

Hasil:

```
PONG
```

#### Cek di WordPress:

- Menu: **Settings → Redis**
- Status: **Connected ✅**

---

### ✅ 4. Data Persistence

Test:

```bash
docker-compose down
docker-compose up -d
```

✔ Data tetap ada → volume berhasil

---

## 📸 Screenshot (WAJIB DILAMPIRKAN)

Tambahkan screenshot berikut:

1. Halaman instalasi WordPress
2. Dashboard WordPress
3. Hasil `docker ps` (3 container running)
4. Redis status (Connected)
5. Redis CLI (`PONG`)

---

## 📦 Volume (Data Persistence)

Volume digunakan untuk menyimpan data agar tidak hilang saat container restart.

- WordPress: `/var/www/html`
- MySQL: `/var/lib/mysql`

---

## 🔗 Networking

Semua container berada dalam satu network Docker sehingga bisa saling berkomunikasi menggunakan nama service:

- WordPress → MySQL: `mysql`
- WordPress → Redis: `redis`

---

## ⚙️ Environment Variables

### WordPress

- `WORDPRESS_DB_HOST`
- `WORDPRESS_DB_NAME`
- `WORDPRESS_DB_USER`
- `WORDPRESS_DB_PASSWORD`

### MySQL

- `MYSQL_ROOT_PASSWORD`
- `MYSQL_DATABASE`
- `MYSQL_USER`
- `MYSQL_PASSWORD`

---

## ❓ Jawaban Pertanyaan

### 1. Kenapa perlu volume untuk MySQL?

Agar data database tidak hilang ketika container dihentikan atau dihapus.

---

### 2. Apa fungsi `depends_on`?

Untuk memastikan container seperti MySQL dan Redis dijalankan terlebih dahulu sebelum WordPress.

---

### 3. Bagaimana WordPress connect ke MySQL?

Melalui environment variable:

```
WORDPRESS_DB_HOST=mysql
```

WordPress menggunakan nama service sebagai hostname.

---

### 4. Apa keuntungan menggunakan Redis?

- Mempercepat loading website
- Mengurangi beban database
- Menyimpan cache query
- Meningkatkan performa WordPress

---

## 🏁 Kesimpulan

Project ini berhasil:

- Menjalankan WordPress dengan Docker Compose
- Menghubungkan WordPress dengan MySQL
- Mengintegrasikan Redis sebagai cache
- Menggunakan volume untuk persistence
- Menggunakan network Docker untuk komunikasi antar service

---

## 👨‍💻 Author

Nama: Iqbal
Mata Kuliah: Pemrograman Sisi Server

---
