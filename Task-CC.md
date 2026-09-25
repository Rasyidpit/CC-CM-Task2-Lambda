# ☁️ Tugas Praktikum: Pengenalan AWS Lambda (Serverless Computing)

## 💡 Apa itu AWS Lambda?
Bayangkan kamu ingin menjalankan sebuah program, tapi kamu **tidak mau repot mengelola server** (tidak perlu setup OS, update keamanan, atau sewa server mahal).

**AWS Lambda** adalah layanan *Serverless*. Kamu cukup mengupload kode, dan AWS akan menjalankan kode tersebut **hanya saat dipanggil**.
*   **Keuntungan:** Kamu hanya bayar saat kode berjalan (sangat murah!), dan AWS otomatis mengurus infrastruktur servernya.
*   **Analogi:** Seperti lampu otomatis yang hanya menyala saat ada orang di ruangan (deteksi gerak), dan mati otomatis saat tidak ada orang. Kamu tidak perlu membayar tagihan listrik saat ruangan kosong.

---

## 🎯 Tujuan Tugas
Murid dapat membuat aplikasi kalkulator *backend* sederhana yang bisa diakses via URL publik tanpa perlu mengelola server.

---

## 🚀 Langkah-Langkah Praktikum

### 1. Membuat Fungsi Lambda
1. Login ke **AWS Console** dan ketik **"Lambda"** di kolom pencarian.
2. Klik tombol **"Create function"** (tombol oranye).
3. Pilih **"Author from scratch"**.
4. **Function name**: `eskul-cc-kalkulator-api-namasiswa`
5. **Runtime**: Pilih **Python 3.12**.
6. Klik **"Create function"** di bagian bawah.

### 2. Memasukkan Kode Program
1. Di halaman fungsi yang baru dibuat, scroll ke bawah ke bagian **Code source**.
2. Hapus semua isi kode di `lambda_function.py` dan ganti dengan kode berikut:

```python
import json

def lambda_handler(event, context):
    # Mengambil input angka dari URL (?a=...&b=...)
    params = event.get('queryStringParameters', {})
    a = int(params.get('a', 0))
    b = int(params.get('b', 0))
    
    hasil = a + b
    
    return {
        'statusCode': 200,
        'headers': {
            "Access-Control-Allow-Origin": "*" # Agar bisa diakses dari browser
        },
        'body': json.dumps({'hasil': hasil})
    }
```
3. Klik tombol **"Deploy"** (tombol biru) untuk menyimpan.

### 3. Membuat URL Publik (Agar bisa diakses di Browser)
1. Klik tab **"Configuration"** di bawah nama fungsi.
2. Di menu samping kiri, klik **"Function URL"**.
3. Klik tombol **"Create function URL"**.
4. Di bagian **Auth type**, pilih **"NONE"** (ini agar siapa saja bisa mengakses).
5. Klik **"Save"**.
6. **PENTING**: Di halaman Function URL yang sama, klik **"Edit"** pada bagian **"Configure cross-origin resource sharing (CORS)"**.
7. Centang **"Allow all origins (*)"** dan klik **"Save"**.
8. Kamu akan melihat link seperti: `https://[id].lambda-url.[region].on.aws/`. **Salin URL ini.**

### 4. Mengetes Hasil
1. Download file `index.html` dari repositori ini ke komputermu.
2. Buka file `index.html` menggunakan Text Editor (Notepad/VS Code).
3. Cari baris: `const url = "https://URL_LAMBDA_KAMU_DISINI/?a=" + a + "&b=" + b;`
4. Ganti `https://URL_LAMBDA_KAMU_DISINI/` dengan URL Lambda yang kamu salin di Langkah 3. Simpan filenya.
5. Buka file `index.html` tersebut di browser.
6. Masukkan dua angka, klik **Hitung**, dan lihat hasilnya!

---

## ⚠️ PENTING: Pembersihan (Wajib!)
Setelah sesi selesai, **WAJIB** hapus fungsi agar tidak ada biaya:
1. Masuk ke dashboard **Lambda**.
2. Klik fungsi `eskul-cc-kalkulator-api-namasiswa` yang tadi dibuat.
3. Klik tombol **"Actions"** (kanan atas) -> **"Delete function"**.
4. Konfirmasi dengan mengetik "delete".
