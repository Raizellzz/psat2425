# PSAT2425 - Aplikasi Manajemen Data Siswa

Aplikasi web sederhana berbasis PHP & MySQL untuk mengelola data siswa. Dapat dijalankan di AWS menggunakan EC2 dan RDS.

---

## 📦 Fitur

- Login Admin
- Dashboard siswa
- Tambah/Edit/Hapus data siswa
- Upload file
- Logout

---

## 🚀 Cara Menjalankan di AWS

### 1. Siapkan Server EC2

- Buat instance EC2 dengan OS Linux (contoh: Ubuntu atau Amazon Linux 2)
- Pastikan Security Group mengizinkan akses:
  - HTTP (port 80)
  - SSH (port 22)

### 2. Siapkan Database RDS MySQL

- Buat database RDS MySQL di AWS
- Simpan informasi berikut:
  - **Endpoint**
  - **Nama database**
  - **Username**
  - **Password**

### 3. Konfigurasi EC2 (Contoh: Ubuntu)

Saat membuat instance EC2, pilih pengaturan berikut:

- **Name** = (nama instance)
- **Application and OS Images** = Ubuntu
- **Instance type** = t2.micro atau t2.nano
- **Key pair** = `vockey`
- **Security groups** = Izinkan akses ke SSH, HTTP, HTTPS dari `0.0.0.0/0`

#### Isi *User data* dengan script berikut:

```bash
#!/bin/bash
sudo apt update -y
sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client
sudo rm -rf /var/www/html/{*,.*}
sudo git clone https://github.com/Shirou25/psat2425.git /var/www/html
sudo chmod -R 777 /var/www/html
echo DB_USER=(username) > /var/www/html/.env
echo DB_PASS=(password) >> /var/www/html/.env
echo DB_NAME=(database) >> /var/www/html/.env
echo DB_HOST=(endpoint rds) >> /var/www/html/.env

Ganti (username), (password), (database), dan (endpoint rds) dengan informasi RDS Anda.

4. Konfigurasi Database RDS
Template = Free Tier

Engine = MySQL

Availability = Single-AZ

DB cluster identifier = (nama database)

Master username = (username)

Master password = (password)

Public access = No

Security Group = Izinkan inbound MySQL (port 3306) dari 0.0.0.0/0

🌐 Akses Aplikasi
Buka browser dan akses:

cpp
Salin
Edit
http://<public-ip-ec2>/
🔐 Login Admin
Username: admin

Password: 123
