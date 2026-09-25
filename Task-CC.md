# ☁️ Tugas Praktikum: Kalkulator Serverless (AWS Lambda)

## 💡 Apa itu Serverless?
Kita akan membuat aplikasi **Kalkulator Cloud**. Kamu tidak perlu menyiapkan server sama sekali. Kamu cukup menulis kode untuk menjumlahkan angka, dan AWS yang akan menjalankan kode tersebut saat kamu menekan tombol di website!

---

## 🚀 Langkah 1: Membuat Backend di AWS Lambda
1. Buka **AWS Lambda** di Console -> **Create function**.
2. **Nama**: `eskul-cc-kalkulator-api`, **Runtime**: **Python 3.12**.
3. Klik **Create function**.
4. Di bagian **Code source**, hapus semua kode dan masukkan kode ini:

```python
import json

def lambda_handler(event, context):
    # Mengambil input angka dari query string
    params = event.get('queryStringParameters', {})
    a = int(params.get('a', 0))
    b = int(params.get('b', 0))
    
    hasil = a + b
    
    return {
        'statusCode': 200,
        'headers': {
            "Access-Control-Allow-Origin": "*" # Penting agar bisa diakses dari browser
        },
        'body': json.dumps({'hasil': hasil})
    }
```
5. Klik **Deploy**.
6. Pergi ke tab **Configuration** -> **Function URL** -> **Create function URL**.
7. Pilih **Auth type: NONE**.
8. **PENTING**: Di tab Configuration yang sama, cari menu **"Function URL"** -> Klik edit pada bagian **"Configure cross-origin resource sharing (CORS)"**, centang **"Allow all origins (*)"** dan Simpan. (Ini agar website bisa memanggil Lambda kamu).

---

## 🚀 Langkah 2: Membuat Frontend (UI)
Simpan kode di bawah sebagai `index.html` di komputermu, lalu buka file tersebut di browser:

```html
<!DOCTYPE html>
<html>
<body>
    <h2>Kalkulator Cloud</h2>
    <input type="number" id="a" placeholder="Angka 1"> + 
    <input type="number" id="b" placeholder="Angka 2">
    <button onclick="hitung()">Hitung</button>
    <h3 id="hasil">Hasil: -</h3>

    <script>
        async function hitung() {
            const a = document.getElementById('a').value;
            const b = document.getElementById('b').value;
            // GANTI URL DI BAWAH DENGAN FUNCTION URL LAMBDA KAMU!
            const url = "https://URL_LAMBDA_KAMU_DISINI/?a=" + a + "&b=" + b;
            
            const response = await fetch(url);
            const data = await response.json();
            document.getElementById('hasil').innerText = "Hasil: " + data.hasil;
        }
    </script>
</body>
</html>
```

---

## ⚠️ Pembersihan
Setelah selesai, jangan lupa **Delete** fungsi Lambda kamu di dashboard!
