# 🖥️ Node Exporter Setup on Ubuntu (VirtualBox)

Dokumentasi ini menjelaskan langkah-langkah instalasi dan konfigurasi **Node Exporter** di Ubuntu Server (dalam VirtualBox), digunakan untuk mengumpulkan metrik hardware & OS yang nantinya bisa dipantau dengan Prometheus.

---

## 🔧 Tools & Versi

- OS: Ubuntu Server 22.04 (CLI mode)
- Node Exporter: v1.8.1
- Prometheus: (opsional, untuk integrasi)
- VirtualBox sebagai VM

---

## 📦 Instalasi Node Exporter

1. **Unduh dan Ekstrak**
   ```bash
   cd /tmp
   wget https://github.com/prometheus/node_exporter/releases/download/node_exporter/node_exporter-1.9.1.linux-amd64.tar.gz

   # Ekstrak file yang sudah diunduh
   tar xvfz node_exporter-1.9.1.linux-amd64.tar.gz
   
   sudo mv node_exporter-1.9.1.linux-amd64/node_exporter /usr/local/bin/
   ```

2. **Tambahkan User**
   ```bash
   sudo useradd -rs /bin/false node_exporter
   ```

3. **Buat Service Systemd**
   ```bash
   sudo nano /etc/systemd/system/node_exporter.service
   ```

   Tempel konfigurasi:
   ```bash
   [Unit]
   Description=Node Exporter
   Wants=network-online.target
   After=network.target

   [Service]
   User=node_exporter
   Group=node_exporter
   Type=simple
   ExecStart=/usr/local/bin/node_exporter

   [Install]
   WantedBy=multi-user.target
   ```

4. **Aktifkan & Jalankan**
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable node_exporter
   sudo systemctl start node_exporter
   ```

## 🌐 Akses Metrik Node Exporter
- Cek Status
  ```bash
  sudo systemctl status node_exporter
  ```
- Buka di browser [http://localhost:9100/metrics](http://localhost:9100/metrics)
  Jika berhasil akan memunculkan output:
  ```bash
  # HELP node_cpu_seconds_total ...
  # TYPE node_cpu_seconds_total counter
  node_cpu_seconds_total{cpu="0",mode="idle"} 25483.48
  ...
  ```

## 🔌 Konfigurasi Prometheus untuk Mengambil Metrik 
```bash
# Sesuaikan path ke prometheus.yml di server Prometheus Anda
sudo nano /etc/prometheus/prometheus.yml
```
Tambahkan blok job baru di bawah bagian scrape_configs (atau sesuaikan jika sudah ada konfigurasi serupa):
```bash
- job_name: 'node_exporter'
    static_configs:
      - targets: ['<VM_IP_ADDRESS>:9100'] # Ganti <VM_IP_ADDRESS> dengan IP Ubuntu Server Anda
```
```bash
sudo systemctl restart prometheus
```
