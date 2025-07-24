# 🖥️ Membuat Virtual Machine Ubuntu Server di VirtualBox

## 🎯 Tujuan
Dokumentasi ini menjelaskan langkah-langkah membuat Virtual Machine (VM) untuk Ubuntu Server (CLI) menggunakan VirtualBox. Cocok digunakan untuk keperluan DevOps dan simulasi server environment.

---

## 📋 Prasyarat

- **VirtualBox**  
  Unduh dan instal dari:  
  👉 https://www.virtualbox.org/

- **File ISO Ubuntu Server (CLI)**  
  Unduh dari:  
  👉 https://ubuntu.com/download/server  
  Contoh file: `ubuntu-24.04.2-live-server-amd64.iso`

---

## ⚙️ Langkah-Langkah

### 1. Buat VM Baru
- Buka **VirtualBox**
- Klik tombol **New / Baru**
- Isi:
  - **Name**: `Ubuntu-DevOps`
  - **Type**: `Linux`
  - **Version**: `Ubuntu (64-bit)`
- Klik **Next**

### 2. Atur Memory (RAM)
- Minimum: **2048 MB**
- Rekomendasi: **4096 MB**
- Klik **Next**

### 3. Buat Virtual Hard Disk
- Pilih: `Create a virtual hard disk now`
- Klik **Create**

### 4. Tipe Hard Disk
- Pilih: `VDI (VirtualBox Disk Image)`
- Klik **Next**

### 5. Ukuran Disk
- Masukkan: **30 GB**
- Klik **Create**

### 6. Pasang File ISO Ubuntu Server
- Pilih VM → Klik **Settings**
- Masuk ke tab **Storage**
- Klik `Empty` → Klik ikon CD → **Choose a disk file**
- Pilih file `.iso` Ubuntu Server
- Klik **OK**

### 7. Jalankan VM
- Klik **Start**

---

## 🔧 8. Instalasi Ubuntu Server (Subiquity CLI)

1. **Welcome**: Pilih bahasa → `Enter`  
2. **Keyboard**: Biarkan default → `Done`  
3. **Update Installer**: Pilih `Continue without updating`  
4. **Network**: Pastikan DHCP aktif → `Done`  
5. **Proxy**: Biarkan kosong → `Done`  
6. **Mirror**: Default → `Done`  
7. **Storage**: Gunakan seluruh disk → `Continue`  
8. **Profile Setup**:
   - Name: `devopsuser`
   - Server name: `ubuntu-devops`
   - Username: `devops`
   - Password: isi dan konfirmasi
9. **SSH Setup**: Centang `Install OpenSSH server`  
10. **Snap**: Lewati → `Done`  
11. Tunggu instalasi selesai → pilih **Reboot now**  
12. Keluarkan ISO:
    - **Devices → Optical Drives → Remove disk**
    - Tekan `Enter` di VM

---

## 📦 Langkah Selanjutnya

- Instal & Konfigurasi:
  - Grafana
  - Prometheus
  - Node Exporter
  - Nginx / HAProxy
  - GitLab

---

## ✍️ Penulis

- **Nama**: Diaz Ramadhiani  
- **Tanggal**: Juli 2025  
- **Deskripsi**: Setup awal VirtualBox Ubuntu Server untuk keperluan DevOps.

