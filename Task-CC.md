# ☁️ Tugas Praktikum: Kalkulator Serverless (AWS Lambda)

## 💡 Apa itu Serverless?
Kita akan membuat aplikasi **Kalkulator Cloud**. Kamu tidak perlu menyiapkan server sama sekali. Kamu cukup menulis kode untuk menjumlahkan angka, dan AWS yang akan menjalankan kode tersebut saat kamu menekan tombol di website!

---

## 🚀 Langkah 1: Membuat Backend di AWS Lambda
1. Buka **AWS Lambda** di Console -> **Create function**.
2. **Nama**: `eskul-cc-kalkulator-[nama-siswa]`, **Runtime**: **Python 3.12**.
3. Klik **Create function**.
4. Di bagian **Code source**, hapus semua kode dan masukkan kode ini (tanpa header CORS):

```python
import json

def lambda_handler(event, context):
    params = event.get('queryStringParameters', {})
    try:
        a = int(params.get('a', 0))
        b = int(params.get('b', 0))
        hasil = a + b
    except:
        hasil = 0
    
    return {
        'statusCode': 200,
        'body': json.dumps({'hasil': hasil})
    }
```
5. Klik **Deploy**.
6. Pergi ke tab **Configuration** -> **Function URL** -> **Create function URL**.
7. Pilih **Auth type: NONE**.
8. **PENTING (CORS)**: Klik Edit pada bagian **CORS**, centang **"Allow all origins (*)"**, lalu **Save**.
9. **Salin URL Lambda** yang muncul (https://...).

---

## 🚀 Langkah 2: Upload UI ke S3 Bucket
*Agar aplikasi berjalan lancar, kita harus menaruh `index.html` di S3, tidak boleh dibuka langsung dari laptop.*

1. Edit file `index.html` di komputermu. Cari bagian:
   `const LAMBDA_URL = "ISI_URL_LAMBDA_KAMU_DISINI";`
   Ganti dengan URL Lambda yang kamu salin tadi.
2. Buka **S3** -> pilih bucket `eskul-cc-[nama-siswa]-2026`.
3. Klik **Upload**, masukkan file `index.html` yang sudah diedit.
4. Setelah upload, buka file tersebut di S3, klik tab **Permissions**, pastikan sudah diatur agar **Publicly Accessible**.
5. Buka tab **Properties**, scroll ke bawah ke **Static website hosting**, aktifkan (enable) dan klik **Save**.
6. Gunakan **URL Website** yang muncul di sana untuk membuka Kalkulator Cloud-mu!

---

## ⚠️ Pembersihan
Setelah selesai, **WAJIB** hapus fungsi Lambda dan bucket S3 agar tidak ada biaya:
1. **Lambda**: Pilih fungsi -> **Actions** -> **Delete function**.
2. **S3**: Hapus isi bucket, lalu **Delete bucket**.
