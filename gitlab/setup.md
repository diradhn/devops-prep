# 🦊 GitLab CE Self-Hosted Setup on Ubuntu Server (VirtualBox)

Dokumentasi ini menjelaskan langkah-langkah untuk menginstal dan mengonfigurasi GitLab Community Edition (CE) secara self-hosted pada Virtual Machine (VM) Ubuntu Server di VirtualBox. Panduan ini cocok untuk simulasi DevOps lokal.
---

## ✅ Prasyarat

Sebelum memulai, pastikan Anda memiliki:
- VirtualBox terinstal di komputer host Anda.
- Ubuntu Server 20.04 (64-bit) terinstal di dalam VM VirtualBox Anda.
- Akses sudo atau root di dalam VM.
- Koneksi internet di dalam VM.
- Pengaturan Port Forwarding di VirtualBox VM Anda. Sebagai contoh, Anda bisa meneruskan port HTTP dari VM ke host:
  - Host Port: 8929
  - Guest Port: 8929 (untuk GitLab)

---

## ⚙️ 1. Update System

```bash
sudo apt update && sudo apt upgrade -y
```

## 🐧 2. Install Dependencies
```bash
sudo apt install -y curl openssh-server ca-certificates tzdata perl
```
Tambahkan repositori GitLab CE
```bash
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```

## 📦 3. Install GitLab CE
```bash
sudo EXTERNAL_URL="http://localhost:8929" apt install gitlab-ce -y
```

## 🔧 4. Konfigurasi Port GitLab (Opsional, Jika Diperlukan Penyesuaian)
```bash
sudo nano /etc/gitlab/gitlab.rb
```
Cari baris external_url dan sesuaikan nilainya (jika berbeda dari yang sudah diatur saat instalasi):
```bash
external_url 'http://localhost:8929'
```
Lakukan reconfigure GitLab agar perubahan diterapkan:
```bash
sudo gitlab-ctl reconfigure
```

## 🌐 5. Access GitLab Web UI
Akses melalui: [http://localhost:8929](http://localhost:8929)

## 🔑 6. First Login
Dapatkan kata sandi root awal:
```bash
sudo cat /etc/gitlab/initial_root_password
```
Gunakan username: root dan kata sandi yang baru saja Anda dapatkan.
