# 📊 Instalasi Grafana di Ubuntu Server (CLI)

Dokumentasi ini menjelaskan langkah-langkah instalasi Grafana OSS (Open Source) pada Ubuntu Server di VirtualBox.

---

## ✅ Prasyarat

Pastikan sistem telah diperbarui dan memiliki akses `root` atau `sudo`.

```bash
sudo apt update && sudo apt upgrade -y
```

## 🧰 1. Tambahkan repository Grafana resmi
Langkah pertama adalah menambahkan kunci GPG Grafana dan repositorinya ke sistem Anda.
``` bash
# Tambahkan kunci GPG Grafana
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://apt.grafana.com/gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/grafana.gpg

# Tambahkan repositori Grafana ke sources list Anda
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee /etc/apt/sources.list.d/grafana.list
```

## 📦 2. Instal Grafana
Setelah repositori ditambahkan, Anda bisa menginstal Grafana.
``` bash
sudo apt update
sudo apt install grafana -y
```

## 🚀 3. Jalankan dan aktifkan service Grafana
Setelah instalasi selesai, jalankan dan aktifkan layanan Grafana agar otomatis berjalan saat sistem dinyalakan.
``` bash
sudo systemctl daemon-reexec
sudo systemctl enable grafana-server
sudo systemctl start grafana-server
```
Cek status:
``` bash
sudo systemctl status grafana-server
```

## 🌐 4. Akses Grafana via Browser
Grafana sekarang sudah terinstal dan berjalan. Anda bisa mengaksesnya dari browser host Anda.
Akses dari browser host-mu: [http://localhost:3000](http://localhost:3000)

Default login:
- Username: admin
- Password: admin

## ✅ Selesai
Grafana siap digunakan untuk memvisualisasikan data dari Prometheus, Node Exporter, atau data source lain.
