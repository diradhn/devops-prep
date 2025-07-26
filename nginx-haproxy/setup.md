# 📘 Setup NGINX sebagai Reverse Proxy untuk Prometheus & Grafana
## 📌 Overview
Panduan ini menjelaskan cara mengonfigurasi Nginx sebagai reverse proxy untuk mengarahkan trafik dari single entry point ke aplikasi Prometheus dan Grafana yang berjalan pada port yang berbeda.
```bash
- Prometheus: Akan diakses melalui localhost:9090
- Grafana: Akan diakses melalui localhost:3000
```
## 🧱 Prasyarat
- Ubuntu (VM/Host)
- Layanan Prometheus sudah berjalan di localhost:9090
- Layanan Grafana sudah berjalan di localhost:3000

## 🧪 Step-by-Step Installation
1. Instalasi Nginx
   ```bash
   sudo apt update
   sudo apt install nginx -y
   ```

2. Memulai dan Mengaktifkan Nginx
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```
   
3. Konfigurasi Reverse Proxy
   Edit file konfigurasi default Nginx:
   ```bash
   sudo nano /etc/nginx/sites-available/default
   ```
   Di dalam blok server { ... }, tambahkan konfigurasi location berikut:
   ```bash
   location /grafana/ {
       proxy_pass http://localhost:3000/;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header X-Forwarded-Proto $scheme;
   }
   location /prometheus/ {
       proxy_pass http://localhost:9090/;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header X-Forwarded-Proto $scheme;
   }
   ```
   Penting:
   - Pastikan ada trailing slash (/) di akhir proxy_pass http://localhost:3000/ dan http://localhost:9090/ untuk menghindari kesalahan path relatif.
   - Tambahan proxy_set_header X-Forwarded-For dan X-Forwarded-Proto disarankan agar aplikasi backend (Grafana/Prometheus) mendapatkan informasi IP asli klien dan protokol yang digunakan.
   
4. Uji Konfigurasi dan Restart Nginx
   ```bash
   sudo nginx -t
   sudo systemctl restart nginx
   ```
# 📘 Setup HAProxy (Opsional)
## 🧪 Step-by-Step Installation
1. Instalasi HAProxy
   ```bash
   sudo apt update
   sudo apt install haproxy -y
   ```

2. Periksa Versi dan Status HAProxy
   ```bash
   haproxy -v
   sudo systemctl status haproxy
   ```
   
3. Backup dan Edit Konfigurasi HAProxy
   ```bash
   sudo cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.bak
   sudo nano /etc/haproxy/haproxy.cfg
   ```
   Ganti seluruh isi atau tambahkan di bawah bagian defaults:
   ```bash
   frontend http_front
       bind *:8080
       default_backend nginx_back

   backend nginx_back
       balance roundrobin
       server nginx1 127.0.0.1:80 check
   ```
   Penjelasan:
   - frontend menerima request dari luar (port 8080)
   - backend mengarahkan trafik ke Nginx lokal di port 80
   
4. Restart dan Aktifkan HAProxy
   ```bash
   sudo systemctl restart haproxy
   sudo systemctl enable haproxy
   ```
   Setelah itu, buka di browser: [http://localhost:8888](http://localhost:8888)
   Jika muncul halaman Welcome to nginx!, berarti HAProxy berhasil meneruskan request ke Nginx
