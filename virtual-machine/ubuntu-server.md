# 🖥️ Membuat Virtual Machine Ubuntu Server di VirtualBox

## 🎯 Tujuan
Dokumentasi ini menjelaskan langkah-langkah membuat Virtual Machine (VM) untuk Ubuntu Server (CLI) menggunakan VirtualBox. Cocok digunakan untuk keperluan DevOps dan simulasi server environment.

---

## 📋 Prasyarat

- **VirtualBox**
  > Jika belum terinstal, kamu bisa mengunduh dan menginstalnya dari situs resmi:  
  🔗 [https://www.virtualbox.org/](https://www.virtualbox.org/)

- **File ISO Ubuntu Server (CLI)**
  > Unduh versi terbaru Ubuntu Server dari halaman resmi Ubuntu:  
  🔗 [https://ubuntu.com/download/server](https://ubuntu.com/download/server)  
  Contoh file: `ubuntu-24.04.2-live-server-amd64.iso`

---

## ⚙️ Langkah-Langkah

### 1. Membuat VM Baru
- Buka **VirtualBox**
- Klik tombol **New / Baru**
- Isi informasi berikut:
  - **Name**: `Ubuntu-DevOps`
  - **Machine Folder**: default atau sesuai keinginan
  - **Type**: `Linux`
  - **Version**: `Ubuntu (64-bit)`
- Klik **Next**

### 2. Atur Memori (RAM)
- Pilih ukuran RAM:
  - Minimum: **2048 MB (2 GB)**
  - Rekomendasi: **4096 MB (4 GB)**
- Klik **Next**

### 3. Buat Virtual Hard Disk
- Pilih: `Create a virtual hard disk now`
- Klik **Create**

### 4. Pilih Jenis Hard Disk
- Pilih: `VDI (VirtualBox Disk Image)`
- Klik **Next**

### 5. Tipe Alokasi
- Pilih: `Dynamically allocated`
- Klik **Next**

### 6. Ukuran Disk
- Masukkan ukuran disk, contoh: **25 GB**
- Klik **Create**

### 7. Pasang File ISO Ubuntu Server
- Pilih VM yang baru dibuat (`Ubuntu-DevOps`)
- Klik tombol **Settings**
- Masuk ke tab **Storage**
- Klik `Empty` di bagian **Controller: IDE**
- Klik ikon CD di kanan ➝ pilih `Choose a disk file`
- Pilih file ISO Ubuntu Server
- Klik **OK**

### 8. Menjalankan VM
- Klik **Start** (ikon panah hijau)
- Proses instalasi Ubuntu akan dimulai

---

## 🖊️ Penulis
- **Nama**: [Diaz Ramadhiani]
- **Tanggal**: Juli 2025
- **Deskripsi**: Langkah awal menyiapkan environment DevOps dengan membuat VM Ubuntu Server.
