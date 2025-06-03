# README.md

## 📡 Line Monitoring & Daily Report via Email

Script Python untuk melakukan pengecekan latency (RTT) menggunakan `mtr` ke daftar IP dari file Excel, membandingkan dengan ambang batas (threshold), dan mengirim hasilnya melalui email dalam format HTML tabel.

---

### 🧩 Fitur

- Membaca IP dan threshold dari file Excel.
- Menggunakan `mtr` untuk mengukur average RTT.
- Menandai hasil sebagai "OK" atau "Alert" berdasarkan threshold.
- Mengirim laporan harian ke email.
- Bisa dijalankan otomatis via `crontab`.

---

### 🗂️ Format File Excel (`line_list.xlsx`)

File Excel harus memiliki format sebagai berikut:

| IP Address | Threshold (ms) | Line Name |
|------------|----------------|-----------|
| 1.1.1.1    | 50             | MainLine1 |
| 8.8.8.8    | 100            | GoogleDNS |

> Catatan: Header berada di baris pertama. Data dibaca dari baris ke-2.

---

### 🔧 Instalasi

1. **Clone repository ini**:

```bash
git clone https://github.com/ahmad0523/auto-ping-starter.git
cd auto-ping-starter
```

2. **Siapkan virtual environment (opsional)**:

```bash
python3 -m venv venv
source venv/bin/activate
```

3. **Install dependencies**:

```bash
pip install -r requirements.txt
```

4. **Install `mtr` jika belum ada**:

```bash
sudo apt install mtr  # Untuk Debian/Ubuntu
```

---

### ⚙️ Konfigurasi

Edit file `checkline.py`:
- Ganti nilai `sender`, `smtpHost`, `smtpPort`, dan `Password-email`.
- Tambahkan penerima email di list `toAdd`.


### 🕒 Cronjob (Opsional)

Tambahkan cronjob untuk menjalankan script secara otomatis:

```bash
crontab -e
```

Contoh entry cron:

```bash
0 7 * * * /usr/bin/python3 /path/to/auto-ping-starter/checkline.py
```

> Artinya script akan dijalankan setiap hari pukul 07:00.

---

### 📬 Output Email

Email akan dikirim dengan format HTML tabel seperti berikut:

| Line Name | IP Address | Threshold (ms) | Average RTT (ms) | Status |
|-----------|------------|----------------|------------------|--------|
| MainLine1 | 1.1.1.1    | 50             | 48.7             | OK     |
| GoogleDNS | 8.8.8.8    | 100            | 120.3            | Alert  |

---


### 📄 Requirements

openpyxl
numpy


---

### 🤝 Kontribusi

Pull Request dan issue sangat diterima untuk pengembangan lebih lanjut.

---

### 🧪 Testing (opsional)

Untuk melakukan testing lokal:

```bash
python checkline.py
```

Pastikan file `line_list.xlsx` tersedia dan email sudah terkonfigurasi dengan benar.
