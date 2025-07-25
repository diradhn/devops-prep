# 📘 Setup NGINX as Reverse Proxy for Prometheus & Grafana
## 📌 Overview
Nginx digunakan sebagai reverse proxy untuk mengarahkan:
```bash
- ke Prometheus (localhost:9090)
- ke Grafana (localhost:3000)
```
## 🧱 Prerequisites
- Ubuntu (VM/Host)
- Prometheus sudah berjalan di port 9090
- Grafana sudah berjalan di port 3000

## 🧪 Step-by-Step Installation
1. Install Nginx
   ```bash
   sudo apt update
   sudo apt install nginx -y
   ```

2. Start & Enable Nginx
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```
   
3. Konfigurasi Reverse Proxy
   Edit file konfigurasi default Nginx:
   ```bash
   sudo nano /etc/nginx/sites-available/default
   ```
   Tambahkan konfigurasi berikut di dalam blok server { ... }:
   ```bash
   location /grafana/ {
    proxy_pass http://localhost:3000/;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
   }
   location /prometheus/ {
    proxy_pass http://localhost:9090/;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
   }
   ```
   Pastikan trailing slash (/) di akhir proxy_pass ada, untuk menghindari path error.
   
4. Restart Nginx
   ```bash
   sudo systemctl restart nginx
   ```
