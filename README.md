# 📱 Litera-AI Monorepo (Mobile Client, Backend API, & AI Services)

<p align="center">
  <img src="apps/mobile/assets/images/logo.png" alt="Litera-AI Logo" width="120" height="120" />
</p>

[![Flutter](https://img.shields.io/badge/Flutter-3.x-blue?style=for-the-badge&logo=flutter)](https://flutter.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com/)
[![Python](https://img.shields.io/badge/Python-3.10+-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![Docker](https://img.shields.io/badge/Docker-Enabled-blue?style=for-the-badge&logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Active-blue?style=for-the-badge&logo=postgresql)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-Active-red?style=for-the-badge&logo=redis)](https://redis.io/)

---

## 📖 Deskripsi Proyek (Project Description)

**LITERA-AI App** adalah repositori monorepo utama yang mengintegrasikan seluruh layanan klien seluler (mobile client), layanan backend server, serta model kecerdasan buatan (predictive AI) dalam ekosistem **LITERA-AI (Literacy Intelligent Assistant)**. Proyek ini dikembangkan secara komprehensif untuk menyukseskan program **P-LIDM (Platform Inovasi Teknologi AI dengan Asesmen Diagnostik Adaptif)**.

Monorepo ini menggabungkan tiga pilar teknologi utama:
1. **Aplikasi Mobile (Flutter)**: Aplikasi seluler lintas platform (Android & iOS) yang menjadi media utama interaksi siswa dalam melakukan asesmen diagnostik, membaca karya sastra klasik, dan mengerjakan latihan menulis kreatif.
2. **Backend Server (FastAPI)**: Server API asinkron berperforma tinggi yang memproses logika autentikasi, sinkronisasi data luar jaringan (offline synchronization), pengumpulan data keaktifan siswa, dan interaksi basis data.
3. **AI Inference & Decision Engine (Python)**: Modul analitik cerdas yang mengimplementasikan metode *Knowledge Tracing* dan pengambilan keputusan *Dynamic Difficulty Adjustment* (DDA) guna menyesuaikan kesulitan soal kuis sastra secara otomatis sesuai kemampuan adaptif siswa.

Dengan pendekatan terpadu ini, Litera-AI App menjamin pengalaman belajar literasi sastra yang terasa personal, adaptif, dan menyenangkan tanpa melupakan kendala koneksi internet di lapangan melalui sistem *offline-first storage* yang tangguh.

---

## 📂 Struktur Monorepo (Workspace Architecture)

```text
apps/
  ├── mobile/         # Aplikasi seluler berbasis Flutter (Dart)
  ├── backend/        # RESTful API Backend berbasis FastAPI (Python)
  └── ai/             # Modul klasifikasi kognitif & pembuatan keputusan DDA (Python)
docs/                 # Dokumentasi diagram alur, API OpenAPI, ERD Database, & strategi pengujian
infra/                # Konfigurasi orkestrasi Docker Compose dan reverse proxy Nginx
```

### 📐 Arsitektur Sistem (System Architecture)

```mermaid
graph TD
    subgraph Client_Space [Client Space]
        A[Flutter Mobile Client] -->|offline cache| B[(Hive Local Cache)]
        A -->|API Requests| C[Nginx Reverse Proxy]
    end
    subgraph Backend_Server [Backend Server]
        C -->|routes to /api/v1| D[FastAPI Backend Server]
        D -->|asynchronous ORM| E[(PostgreSQL Database)]
        D -->|session caching| F[(Redis Cache)]
    end
    subgraph AI_Engine [AI Engine]
        D -->|triggers KT & DDA| G[Predictive AI Engine]
        G -->|Knowledge Tracing / DDA decisions| D
    end
```

---

## ✨ Fitur Utama Modul (Core Module Features)

### 📱 1. Aplikasi Mobile (Flutter Client)
* **Desain Premium Material 3**: Tema warna yang disesuaikan secara harmonis (Emerald & Light-Dark mode support) untuk menjaga kenyamanan mata siswa saat membaca dalam durasi lama.
* **Offline-First Mode & Sync Banner**: Penyimpanan lokal menggunakan **Hive database** dengan sistem antrian outbox yang persisten. Siswa tetap dapat membaca dan mengerjakan tugas saat offline, dan aplikasi secara otomatis melakukan sinkronisasi data saat mendeteksi internet aktif kembali.
* **Siklus Belajar Adaptif**: Menampilkan perjalanan belajar siswa (*learning paths*), kuis dinamis, papan peringkat gamifikasi (leaderboards), serta riwayat membaca personal.

### ⚡ 2. Backend API (FastAPI Server)
* **Pemrosesan Asinkron Asli**: Memaksimalkan kecepatan respons dengan *async/await* Python melalui SQLAlchemy ORM.
* **Sinkronisasi Endpoint Efisien**: Menerima data payload dari antrian mobile secara batch untuk meminimalkan beban bandwidth seluler.
* **Arsitektur Skalabel**: Migrasi otomatis schema database menggunakan Alembic.

### 🤖 3. Mesin Evaluasi AI (Predictive AI Engine)
* **Diagnostik Profil Kognitif**: Menilai level literasi siswa pasca pengerjaan asesmen awal.
* **Dynamic Difficulty Adjustment (DDA)**: Mengatur parameter tingkat kesulitan kuis berikutnya secara real-time berdasarkan akurasi dan durasi pengerjaan soal siswa sebelumnya.

---

## 🚀 Panduan Menjalankan Layanan (Execution Guide)

### 📱 1. Aplikasi Mobile (Flutter)
```bash
cd apps/mobile
flutter pub get
flutter run
```

### ⚡ 2. Backend Server (FastAPI)
1. Salin konfigurasi environment di `apps/backend/` dan sesuaikan nilainya:
   ```env
   DATABASE_URL="postgresql+asyncpg://postgres:postgres@localhost:5432/litera_backend"
   REDIS_URL="redis://localhost:6379/0"
   ```
2. Setup environment Python dan jalankan server:
   ```bash
   cd apps/backend
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   pip install -e ".[dev]"
   uvicorn app.main:app --reload
   ```

### 🐳 3. Menjalankan via Docker Compose (Rekomendasi Produksi)
Orkestrasikan database PostgreSQL, Redis Cache, Backend API, dan reverse proxy Nginx dengan satu perintah:
```bash
cd infra/docker
docker-compose up -d --build
```
Layanan backend akan secara otomatis terekspos dengan aman melalui reverse proxy Nginx pada port yang ditentukan.

---

## 🎯 Kesimpulan & Kontribusi (Conclusion & Vision)

**LITERA-AI Monorepo** menggabungkan portabilitas tinggi Flutter dengan kecepatan pemrosesan data asinkron FastAPI dan ketepatan prediksi kecerdasan buatan. Integrasi erat antar komponen dalam monorepo ini memastikan pemeliharaan kode (code maintenance) dan siklus integrasi/pengembangan berkelanjutan (CI/CD) berjalan dengan sangat efisien. 

Proyek ini diharapkan mampu berkontribusi nyata dalam menghapus hambatan akses pendidikan, menyajikan asisten belajar sastra berkualitas tinggi yang gratis bagi seluruh siswa di Indonesia, serta mendukung pendidik dalam merancang pembelajaran berbasis data yang tepat sasaran.
