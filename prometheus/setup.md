# 📈 Instalasi dan Setup Prometheus di Ubuntu CLI (VirtualBox)

Dokumentasi ini berisi langkah-langkah lengkap untuk menginstal dan menjalankan **Prometheus** di sistem operasi Ubuntu CLI yang dijalankan melalui VirtualBox.

## 🧰 Prasyarat

- VirtualBox telah terpasang di komputer host
- VM Ubuntu CLI telah berjalan dengan akses `sudo`
- Terhubung ke internet

---

## 📦 Langkah Instalasi Prometheus

### 1. Buat User dan Direktori Prometheus

```bash
sudo useradd --no-create-home --shell /bin/false prometheus
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
```

### 2. Unduh Prometheus
Cek versi terbaru di: [prometheus](https://prometheus.io/download/)
```bash
cd /tmp
wget https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz
tar xvf prometheus-3.5.0.linux-amd64.tar.gz
cd prometheus-3.5.0.linux-amd64
```

### 3. Pindahkan File Biner
```bash
sudo cp prometheus /usr/local/bin/
sudo cp promtool /usr/local/bin/
sudo chown prometheus:prometheus /usr/local/bin/prometheus
sudo chown prometheus:prometheus /usr/local/bin/promtool
```

### 4. Pindahkan File Konfigurasi & Konsol
```bash
sudo cp -r consoles /etc/prometheus
sudo cp -r console_libraries /etc/prometheus
sudo cp prometheus.yml /etc/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus
sudo chown -R prometheus:prometheus /var/lib/prometheus
```

## ⚙️ Buat Service Prometheus
### 1. Buat File Service Systemd
```bash
sudo nano /etc/systemd/system/prometheus.service
```
Isi file dengan:
```bash
[Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target

[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
    --config.file=/etc/prometheus/prometheus.yml \
    --storage.tsdb.path=/var/lib/prometheus/ \
    --web.console.templates=/etc/prometheus/consoles \
    --web.console.libraries=/etc/prometheus/console_libraries

[Install]
WantedBy=multi-user.target
```
Simpan dan keluar (CTRL+O, Enter, lalu CTRL+X)

### 2. Reload & Jalankan Prometheus
```bash
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl start prometheus
sudo systemctl enable prometheus
```

### 3. Cek Status
```bash
sudo systemctl status prometheus
```
Pastikan statusnya active (running)

## 🌐 Akses Prometheus di Browser
Konfigurasi Port Forwarding VirtualBox:
1. Matikan VM Ubuntu CLI
2. Buka VirtualBox → Settings → Network → Advanced → Port Forwarding
3. Tambahkan aturan:
   - Name: Prometheus
   - Protocol: TCP
   - Host Port: 9090
   - Guest Port: 9090

Akses di Browser (Host): [http://localhost:9090](http://localhost:9090)

## ✅ Selesai
Prometheus berhasil diinstal dan dijalankan. Kamu bisa menghubungkannya dengan Node Exporter atau visualisasikan metriknya lewat Grafana.
