# ☁️ Tugas Praktikum: Pengenalan AWS Lambda (Serverless Computing)

## 💡 Apa itu AWS Lambda?
Bayangkan kamu ingin menjalankan sebuah program, tapi kamu **tidak mau repot mengelola server** (tidak perlu setup OS, update keamanan, atau sewa server mahal).

**AWS Lambda** adalah layanan *Serverless*. Kamu cukup mengupload kode, dan AWS akan menjalankan kode tersebut **hanya saat dipanggil**.
*   **Keuntungan:** Kamu hanya bayar saat kode berjalan (sangat murah!), dan AWS otomatis mengurus infrastruktur servernya.
*   **Analogi:** Seperti lampu otomatis yang hanya menyala saat ada orang di ruangan (deteksi gerak), dan mati otomatis saat tidak ada orang. Kamu tidak perlu membayar tagihan listrik saat ruangan kosong.

---

## 🎯 Tujuan Tugas
Murid dapat membuat fungsi *backend* sederhana yang bisa diakses via URL publik tanpa infrastruktur server.

---

## 🚀 Langkah-Langkah Praktikum (Ikuti Perlahan)

### 1. Membuat Fungsi Lambda
1. Login ke **AWS Console** dan ketik **"Lambda"** di kolom pencarian.
2. Klik tombol **"Create function"** (tombol oranye).
3. Pilih **"Author from scratch"**.
4. **Function name**: `eskul-cc-[nama-siswa]-api`
5. **Runtime**: Pilih **Python 3.12**.
6. Klik **"Create function"** di bagian bawah.

### 2. Memasukkan Kode Program
1. Setelah fungsi dibuat, scroll ke bawah ke bagian **Code source**.
2. Hapus semua isi kode di `lambda_function.py` dan ganti dengan kode berikut:

```python
import json

def lambda_handler(event, context):
    # Mengambil parameter 'name' dari URL (jika ada)
    query_params = event.get('queryStringParameters')
    name = query_params['name'] if query_params and 'name' in query_params else "Cloud Learner"
    
    # Pesan respon
    pesan = f"Halo {name}! Selamat datang di Serverless API pertama Anda!"
    
    return {
        'statusCode': 200,
        'body': json.dumps({'message': pesan})
    }
```
3. Klik tombol **"Deploy"** (tombol biru) di atas editor kode untuk menyimpan perubahan.

### 3. Membuat URL Publik (Agar bisa diakses di Browser)
1. Klik tab **"Configuration"** di bawah nama fungsi.
2. Di menu samping kiri, klik **"Function URL"**.
3. Klik tombol **"Create function URL"**.
4. Di bagian **Auth type**, pilih **"NONE"** (ini agar siapa saja bisa mengakses).
5. Klik **"Save"**.
6. Kamu akan melihat link panjang seperti: `https://[id].lambda-url.[region].on.aws/`. Klik link tersebut!

### 4. Mengetes Hasil
1. Saat kamu buka link tadi, website akan menampilkan pesan JSON.
2. Coba tambahkan `?name=Namamu` di akhir URL tersebut di browser.
   * *Contoh*: `https://[id].lambda-url...on.aws/?name=Togar`
3. Lihat perubahannya!

---

## ⚠️ PENTING: Pembersihan (Agar tidak ada tagihan!)
Setelah selesai, hapus fungsi agar akun tetap gratis:
1. Masuk ke dashboard **Lambda**.
2. Klik fungsi `eskul-cc-[nama-siswa]-api` yang tadi dibuat.
3. Klik tombol **"Actions"** (kanan atas) -> **"Delete function"**.
4. Konfirmasi dengan mengetik "delete".
