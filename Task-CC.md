# 🚀 Tugas Cepat: Kalkulator Serverless (AWS Lambda)

## 🎯 Tujuan
Membuat API kalkulator sederhana dalam 5 menit.

## 🚀 Langkah-Langkah (Ikuti cepat!)

### 1. Buat Fungsi Lambda
1. Buka **Lambda** -> **Create function**.
2. **Name**: `kalkulator-[nama-siswa]`, **Runtime**: **Python 3.12**.
3. Klik **Create function**.

### 2. Isi Kode
Di bagian **Code source**, masukkan kode ini dan klik **Deploy**:

```python
import json
def lambda_handler(event, context):
    params = event.get('queryStringParameters', {})
    a = int(params.get('a', 0))
    b = int(params.get('b', 0))
    return {
        'statusCode': 200,
        'body': json.dumps({'hasil': a + b})
    }
```

### 3. Buat URL Publik
1. Klik tab **Configuration** -> **Function URL**.
2. Klik **Create function URL**.
3. Pilih **Auth type: NONE**.
4. Klik **Save**.
5. Salin **Function URL** yang muncul.

### 4. Tes Langsung di Browser
Buka link berikut di browser kamu, lalu tambahkan `?a=10&b=5` di akhir URL tersebut:

`https://[URL-LAMBDA-KAMU]/?a=10&b=5`

Jika muncul `{"hasil": 15}`, **Tugas Selesai!**

---
⚠️ **Wajib Hapus**: Setelah selesai, **Delete** fungsi Lambda kamu agar tidak ada biaya!
