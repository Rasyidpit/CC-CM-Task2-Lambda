# ☁️ Tugas Praktikum: Kalkulator Serverless (AWS Lambda)

## 💡 Apa itu Serverless?
**AWS Lambda** adalah layanan *Serverless*. Kamu cukup mengupload kode, dan AWS akan menjalankan kode tersebut hanya saat dipanggil. Kamu tidak perlu mengatur server sama sekali.

---

## 🎯 Tujuan Tugas
Membuat aplikasi kalkulator interaktif yang berjalan sepenuhnya di cloud dengan AWS Lambda.

---

## 🚀 Langkah-Langkah Praktikum

### 1. Membuat Fungsi Lambda
1. Login ke **AWS Console** -> cari **"Lambda"**.
2. Klik **"Create function"**.
3. Pilih **"Author from scratch"**.
4. **Function name**: `kalkulator-[nama-siswa]`
5. **Runtime**: Pilih **Python 3.12**.
6. Klik **"Create function"**.

### 2. Memasukkan Kode Program
1. Di halaman fungsi, scroll ke **Code source**.
2. Hapus semua isi `lambda_function.py` dan ganti dengan kode di bawah ini.
3. Klik tombol **"Deploy"** (biru) untuk menyimpan.

```python
import json

def lambda_handler(event, context):
    params = event.get('queryStringParameters', {})
    
    # Jika ada angka, lakukan kalkulasi
    if 'a' in params and 'b' in params:
        try:
            hasil = int(params.get('a')) + int(params.get('b'))
            return {
                'statusCode': 200,
                'headers': {"Content-Type": "application/json"},
                'body': json.dumps({'hasil': hasil})
            }
        except:
            return {'statusCode': 400, 'body': 'Input salah'}

    # Jika tidak ada angka, kirim Tampilan (UI) Kalkulator
    html_ui = """
    <!DOCTYPE html>
    <html>
    <head><title>Kalkulator Serverless</title></head>
    <body style="font-family:sans-serif; text-align:center; padding:50px;">
        <h2>Kalkulator Cloud</h2>
        <input type="number" id="a" placeholder="Angka 1"> + 
        <input type="number" id="b" placeholder="Angka 2">
        <button onclick="hitung()">Hitung</button>
        <h3 id="hasil">Hasil: -</h3>
        <script>
            async function hitung() {
                const a = document.getElementById('a').value;
                const b = document.getElementById('b').value;
                const url = window.location.href + "?a=" + a + "&b=" + b;
                const res = await fetch(url).then(r => r.json());
                document.getElementById('hasil').innerText = "Hasil: " + res.hasil;
            }
        </script>
    </body>
    </html>
    """
    return {
        'statusCode': 200,
        'headers': {"Content-Type": "text/html"},
        'body': html_ui
    }
```

### 3. Membuat URL Publik
1. Klik tab **"Configuration"** -> **"Function URL"**.
2. Klik **"Create function URL"**.
3. Pilih **Auth type: NONE**.
4. Klik **"Save"**.
5. Salin **Function URL** yang muncul.

### 4. Mengetes Hasil
1. Buka URL tersebut di browser.
2. Kalkulator akan muncul secara otomatis!
3. Masukkan angka dan klik **Hitung**.

---

## ⚠️ PENTING: Pembersihan (Wajib!)
Setelah selesai, **WAJIB** hapus fungsi agar tidak ada biaya:
1. Masuk dashboard **Lambda** -> Pilih fungsi -> **Actions** -> **Delete function**.
