Berikut adalah dokumen spesifikasi perangkat lunak yang komprehensif untuk sebuah aplikasi MVP (Minimum Viable Product).

1. Product Requirements Document (PRD)
Nama Produk: TaskFlow - Aplikasi Manajemen Tugas Sederhana
Versi: 1.0 (MVP)
Tanggal: 26 Oktober 2023

1.1. Gambaran Umum (Overview)
TaskFlow adalah aplikasi web sederhana yang membantu individu dan tim kecil untuk mengelola daftar tugas mereka. Fokus MVP adalah pada fungsionalitas inti: membuat, membaca, memperbarui, dan menghapus tugas (CRUD) dengan antarmuka yang intuitif.

1.2. Tujuan (Goals)

Memungkinkan pengguna mencatat tugas mereka di satu tempat.

Meningkatkan produktivitas pengguna dengan memberikan klarifikasi pada tugas yang harus diselesaikan.

Mendapatkan umpan balik pengguna awal untuk pengembangan fitur selanjutnya (seperti kolaborasi tim, tenggat waktu, dll.).

1.3. Persona Pengguna (User Personas)

Andi (Freelancer): Sibuk dengan banyak proyek dari klien berbeda. Butuh工具 untuk melacak milestone setiap proyek agar tidak ada yang terlewat.

Sari (Mahasiswa): Memiliki banyak tugas kuliah, jadwal kelompok, dan target belajar. Butuh工具 untuk mengatur prioritas.

1.4. Fitur-Fitur (Features)
F1: Manajemen Tugas (Core)

F1.1: Pengguna dapat membuat tugas baru dengan mengisi judul (wajib) dan deskripsi (opsional).

F1.2: Pengguna dapat melihat semua tugasnya dalam satu daftar.

F1.3: Pengguna dapat menandai tugas sebagai "Selesai" atau "Belum Selesai".

F1.4: Pengguna dapat mengedit judul dan deskripsi tugas yang sudah dibuat.

F1.5: Pengguna dapat menghapus tugas.

F2: Antarmuka Pengguna (UI)

F2.1: Tampilan daftar tugas yang clean dan responsif (bisa digunakan di desktop dan mobile).

F2.2: Tampilan form untuk menambah dan mengedit tugas.

F2.3: Feedback yang jelas saat sebuah tindakan berhasil (e.g., "Tugas berhasil ditambahkan") atau gagal.

F3: Manajemen Status (State Management)

F3.1: Aplikasi harus menyimpan status tugas (selesai/belum) meskipun browser ditutup dan dibuka kembali (menggunakan localStorage atau database sederhana).

1.5. Metrik Kesuksesan (Success Metrics)

Penggunaan Aktif Harian (DAU): Rata-rata 5 pengguna yang kembali menggunakan aplikasi dalam sehari.

Rasio Penyelesaian Tugas: 70% tugas yang dibuat ditandai sebagai "Selesai".

Umpan Balik Pengguna: Mengumpulkan setidaknya 20 masukan dari pengguna beta mengenai fitur yang mereka inginkan selanjutnya.

2. Entity Relationship Diagram (ERD)
Untuk MVP, struktur datanya sangat sederhana karena hanya memiliki satu entity utama.

Entities:

Tasks

id (Integer, Primary Key, Auto-Increment)

title (String, Required)

description (Text, Optional)

is_completed (Boolean, Default: false)

created_at (DateTime, Default: Current Timestamp)

updated_at (DateTime, Default: Current Timestamp on Update)

ERD Diagram:

text
+-----------------------+
|        Tasks          |
+-----------------------+
| id (PK) INT           |
| title VARCHAR(255)    |
| description TEXT      |
| is_completed BOOLEAN  |
| created_at DATETIME   |
| updated_at DATETIME   |
+-----------------------+
(Catatan: Untuk MVP, autentikasi pengguna belum ada, jadi semua tugas disimpan dalam satu pool. Untuk produksi, perlu ditambahkan entity Users dan relationship user_id).

3. Software Requirements Specification (SRS)
1. Pendahuluan
Dokumen ini mendefinisikan semua persyaratan fungsional dan non-fungsional untuk TaskFlow v1.0 (MVP).

2. Persyaratan Fungsional (Functional Requirements)

ID	Requirement Description	Prioritas
FR1	Sistem harus menyediakan form input dengan field "Judul Tugas" (wajib) dan "Deskripsi" (opsional).	Tinggi
FR2	Sistem harus memungkinkan pengguna menyimpan tugas, yang kemudian ditampilkan dalam daftar.	Tinggi
FR3	Di dalam daftar, setiap tugas harus menampilkan: Judul, Deskripsi (jika ada), dan checkbox status.	Tinggi
FR4	Sistem harus memperbarui status tugas (selesai/belum selesai) saat pengguna mengklik checkbox.	Tinggi
FR5	Sistem harus menyediakan tombol atau link "Edit" pada setiap tugas yang mengarah ke form pre-populated untuk edit.	Medium
FR6	Sistem harus memperbarui tugas di daftar setelah penyuntingan.	Medium
FR7	Sistem harus menyediakan tombol atau link "Hapus" pada setiap tugas yang memunculkan konfirmasi.	Medium
FR8	Sistem harus menghapus tugas dari daftar setelah konfirmasi.	Medium
FR9	Data tugas harus bertahan (persisten) di browser pengguna setelah halaman direfresh atau ditutup.	Tinggi
3. Persyaratan Non-Fungsional (Non-Functional Requirements)

ID	Requirement Description
NFR1	Usability: Antarmuka harus mudah dipahami dan digunakan oleh pengguna non-teknis dalam 5 menit.
NFR2	Performance: Daftar tugas harus loading dalam waktu kurang dari 2 detik.
NFR3	Compatibility: Aplikasi harus dapat dijalankan di browser modern (Chrome, Firefox, Safari, Edge).
NFR4	Reliability: Aplikasi tidak boleh crash karena input yang tidak valid.
4. Software Design Document (SDD)
1. Arsitektur Sistem

Frontend: Aplikasi Single-Page (SPA) menggunakan HTML, CSS, dan JavaScript vanilla (atau React/Vue.js sederhana untuk keteraturan kode).

State Management: Data akan disimpan di dalam localStorage browser pengguna. Tidak ada backend server untuk MVP ini.

Build Tool: Untuk kesederhanaan, tidak diperlukan tool seperti Webpack. File JavaScript modular sudah cukup.

2. Desain UI/UX

Wireframe: Daftar tugas di bagian atas, form input di bawahnya. Setiap item tugas memiliki: [Checkbox] [Judul] [Tombol Edit] [Tombol Hapus]. Klik judul/deskripsi mungkin untuk melihat detail.

Teknologi UI: HTML5, CSS3 (dengan Flexbox/Grid untuk layout), JavaScript.

3. Desain Teknis & Pseudocode

Struktur Data:

javascript
// Array of task objects akan disimpan di localStorage
let tasks = [
    {
        id: 1, // Timestamp bisa digunakan sebagai ID
        title: "Belajar JavaScript",
        description: "Baca bab 5 dan kerjakan latihan",
        is_completed: false,
        created_at: 1698312000,
        updated_at: 1698312000
    }
];
Fungsi Utama:

javascript
// Pseudocode untuk fungsi utama
function saveTask(taskData) {
    validasi taskData;
    generate ID dan timestamp;
    tambahkan objek task baru ke array `tasks`;
    simpan array `tasks` yang telah diupdate ke localStorage;
    update UI;
}

function loadTasks() {
    ambil data dari localStorage;
    parse data JSON menjadi array;
    render setiap task ke dalam DOM;
}

function updateTaskStatus(taskId, newStatus) {
    cari task dalam array `tasks` berdasarkan taskId;
    update property `is_completed` dan `updated_at`;
    simpan array `tasks` yang telah diupdate ke localStorage;
    update UI (e.g., coret judul task);
}

function deleteTask(taskId) {
    konfirmasi penghapusan;
    filter task dengan ID tersebut keluar dari array `tasks`;
    simpan array `tasks` yang telah diupdate ke localStorage;
    hapus elemen task dari DOM;
}
5. Checklist Timeline Sprint MVP
Asumsi: Sprint 2 minggu (10 hari kerja)

Week 1: Foundation & Core Functionality

Hari	Tugas	Status (✓)
1	Setup Project: Repositori Git, struktur folder, file HTML, CSS, JS dasar.	
2	Desain UI Dasar: Implementasi layout daftar dan form input berdasarkan wireframe.	
3	Fungsi CRUD - Create & Read: Implementasi saveTask() dan loadTasks().	
4	Fungsi CRUD - Update: Implementasi updateTaskStatus() (checkbox).	
5	Fungsi CRUD - Delete: Implementasi deleteTask().	
Week 2: Polish, Testing, & Deployment

Hari	Tugas	Status (✓)
6	Penyuntingan Tugas: Implementasi form edit dan fungsi updateTask().	
7	Error Handling & Feedback: Tambahkan alert/notifikasi untuk sukses/gagal. Validasi input.	
8	Testing Intensif: Manual testing semua alur pengguna (UX) di berbagai browser.	
9	Bug Fixing: Perbaikan bug yang ditemukan selama testing.	
10	Deployment: Hosting aplikasi di platform sederhana (e.g., Netlify, Vercel, GitHub Pages).	
Definition of Done (DoD) untuk Setiap Tugas:



(Jika applicable) Perubahan telah di-test secara manual.# tugas.1-membuat-dokumen-spesifikasi-perangkat-lunak
