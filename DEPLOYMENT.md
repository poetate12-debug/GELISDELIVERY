# GELIS DELIVERY - Hostinger Deployment Guide

## Overview
GELIS DELIVERY adalah aplikasi pesan antar makanan yang dibangun dengan React + TypeScript dan backend Supabase.

## Prerequisites
- Hostinger account dengan akses SSH/cPanel
- Domain yang sudah dikonfigurasi
- Node.js 18.x atau lebih tinggi (jika menggunakan Hostinger VPS)

## Build & Deployment

### 1. Build Application
```bash
# Clone repository
git clone https://github.com/poetate12-debug/GELISDELIVERY.git
cd GELISDELIVERY

# Install dependencies
npm install

# Build for production
npm run build

# Atau gunakan script build khusus
chmod +x build-hostinger.sh
./build-hostinger.sh
```

### 2. Upload ke Hostinger

#### Method A: cPanel File Manager
1. Login ke cPanel Hostinger
2. Buka "File Manager"
3. Upload semua file dari folder `dist` ke `public_html`
4. Pastikan file `.htaccess` terupload

#### Method B: FTP/SFTP
1. Gunakan FTP client (FileZilla, Cyberduck, dll)
2. Connect ke server Hostinger
3. Upload folder `dist` ke `public_html`

#### Method C: SSH (untuk VPS)
```bash
# Upload ke server
scp -r dist/* user@yourdomain.com:/home/user/public_html/
```

### 3. Konfigurasi Environment Variables
Di Hostinger cPanel, tambahkan environment variables berikut:
```
VITE_SUPABASE_URL=https://eozdslszmuiamycpsepe.supabase.co
VITE_SUPABASE_PUBLISHABLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6ImVvemRzbHN6bXVpYW15Y3BzZXBlIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NjU0OTYwMTYsImV4cCI6MjA4MTA3MjAxNn0.DK4yBbNfnccH-IC2v-p3-tJtBVVYXvTcvLGB43qxPi0
```

### 4. Test Deployment
Buka browser dan kunjungi domain Anda. Aplikasi harusnya sudah berjalan.

## Troubleshooting

### Masalah 1: Halaman 404 pada refresh
- Pastikan file `.htaccess` terupload dengan benar
- Cek konfigurasi Apache di Hostinger

### Masalah 2: Supabase connection error
- Verifikasi environment variables
- Pastikan Supabase URL dan key benar

### Masalah 3: Blank page
- Buka browser developer console
- Cek JavaScript errors
- Pastikan semua assets terupload dengan benar

## File Structure di Hostinger
```
public_html/
├── index.html
├── .htaccess
├── assets/
│   ├── index-abc123.js
│   ├── index-def456.css
│   └── icons/
└── deployment-info.txt
```

## Performance Optimization
- Gzip compression aktif via .htaccess
- Static assets di-cache selama 1 tahun
- Code splitting untuk load yang lebih cepat
- Security headers sudah dikonfigurasi

## SSL Certificate
Hostinger menyediakan SSL certificate gratis. Pastikan:
- SSL aktif di domain Anda
- Redirect HTTP ke HTTPS (bisa ditambahkan di .htaccess)

## Monitoring
- Gunakan Hostinger analytics untuk monitoring traffic
- Monitor error logs di cPanel
- Test aplikasi secara berkala

## Update Deployment
Untuk update aplikasi:
1. Build ulang aplikasi dengan `npm run build`
2. Upload file-file baru ke Hostinger
3. Clear browser cache

## Support
- Hostinger documentation: https://www.hostinger.com/tutorials
- React deployment guide: https://reactjs.org/docs/deployment.html
- Supabase documentation: https://supabase.com/docs