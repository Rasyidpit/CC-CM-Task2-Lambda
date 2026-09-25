# ☁️ Tugas Praktikum: Pengenalan AWS Lambda (Serverless Computing)

## 💡 Apa itu AWS Lambda?
Bayangkan kamu ingin menjalankan sebuah program, tapi kamu **tidak mau repot mengelola server**.

**AWS Lambda** adalah layanan *Serverless*. Kamu cukup mengupload kode, dan AWS akan menjalankan kode tersebut **hanya saat dipanggil**. Kamu hanya membayar ketika kode berjalan, tidak ada biaya server saat tidak digunakan.

---

## 🎯 Tujuan Tugas
Murid dapat membuat aplikasi kalkulator *backend* sederhana yang bisa diakses via URL publik tanpa perlu mengelola server.

---

## 🚀 Langkah-Langkah Praktikum

### 1. Membuat Fungsi Lambda
1. Login ke **AWS Console** dan ketik **"Lambda"** di kolom pencarian.
2. Klik **"Create function"**.
3. Pilih **"Author from scratch"**.
4. **Function name**: `eskul-cc-kalkulator-[nama-siswa]`
5. **Runtime**: Pilih **Python 3.12**.
6. Klik **"Create function"**.

### 2. Memasukkan Kode Program
1. Di halaman fungsi, scroll ke bagian **Code source**.
2. Hapus semua isi kode di `lambda_function.py` dan ganti dengan kode berikut:

```python
import json

def lambda_handler(event, context):
    # Mengambil parameter 'a' dan 'b' dari URL
    params = event.get('queryStringParameters', {})
    try:
        a = int(params.get('a', 0))
        b = int(params.get('b', 0))
        hasil = a + b
    except:
        hasil = 0
    
    return {
        'statusCode': 200,
        'headers': {
            "Access-Control-Allow-Origin": "*" # Agar bisa diakses dari browser
        },
        'body': json.dumps({'hasil': hasil})
    }
```
3. Klik tombol **"Deploy"** untuk menyimpan.

### 3. Membuat URL Publik & CORS
1. Klik tab **"Configuration"** -> **"Function URL"**.
2. Klik **"Create function URL"**.
3. Pilih **Auth type: NONE**.
4. **PENTING (CORS)**: Di halaman yang sama, klik **Edit** pada bagian **CORS**.
5. Centang **"Allow all origins (*)"** dan klik **"Save"**.
6. **Salin URL** yang muncul (contoh: `https://...on.aws/`).

### 4. Mengetes Hasil
1. Download file `index.html` dari repositori ini.
2. Buka `index.html` dengan Text Editor (VS Code/Notepad).
3. Cari baris: `const LAMBDA_URL = "ISI_URL_LAMBDA_KAMU_DISINI";`
4. Ganti teks tersebut dengan URL Lambda yang kamu salin di langkah 3. Simpan.
5. Buka `index.html` di browser dan coba hitung!

---

## ⚠️ PENTING: Pembersihan (Wajib!)
Setelah selesai, **WAJIB** hapus fungsi agar tidak ada biaya:
1. Masuk dashboard **Lambda**.
2. Pilih fungsi tadi -> **Actions** -> **Delete function**.
