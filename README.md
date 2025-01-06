# uas

# Program ini terdiri dari beberapa kelas utama, yaitu Data, view, dan process.

## 1. Kelas Data
Kelas Data digunakan untuk menyimpan informasi pengguna yang terdiri dari Nama, No. Telp, dan Email.

```python
Copy code
class Data_Pendaftaran:
    def __init__(self, name, phone, email):
        self.name = name
        self.phone = phone
        self.email = email
````

## 2. Kelas view
Kelas view bertanggung jawab untuk menangani tampilan dan interaksi dengan pengguna. Kelas ini memiliki beberapa metode:

get_input(): Untuk meminta input dari pengguna (Nama, No. Telp, dan Email).
table_view(data_table): Untuk menampilkan tabel yang berisi data pengguna yang sudah terdaftar.
display_message(message): Untuk menampilkan pesan kepada pengguna.
```python
Copy code
from Data.Data1 import Data_Pendaftaran

class view_pendaftaran:
    def get_input():
        name = input("Nama: ")
        phone = input("No. Telp: ")
        email = input("Email: ")
        return name, phone, email
    
    def table_view(data_table):
        print("="*93)
        print("| NO |               NAMA               |        NO.TELP        |           EMAIL           |")
        print("="*93)
        
        for i, data in enumerate(data_table, start=1):
            print(f"| {i:<2} | {data.name:<32} | {data.phone:<21} | {data.email:<25} |")
        print("="*93)
        
    def display_message(message):
        print(message)
````

## 3. Kelas process
Kelas process berfungsi untuk memvalidasi data yang dimasukkan oleh pengguna. Metode-metode dalam kelas ini adalah:

validate_name(name): Memastikan nama hanya berisi huruf.
validate_phone(phone): Memastikan nomor telepon hanya berisi angka.
validate_email(email): Memastikan email mengikuti format yang benar.
validate_data(data): Menggabungkan semua validasi menjadi satu fungsi untuk memvalidasi seluruh data.

```python
Copy code
import re
from Data.Data1 import Data_Pendaftaran
from View.View1 import view_pendaftaran


class process_pendaftaran:
    def validate_name(name):
        if not name.isalpha:
            raise ValueError("Hanya berisi huruf")
        
    def validate_phone(phone):
        if not phone.isdigit:
            raise ValueError("hanya berisi angka")
        
    def validate_email(email):
        if not re.match(r"[^@]+@[^@]+\.[^@]", email):
            raise ValueError("harus meggunakan huruf '@' & '.'  .")
        
    def validate_data(data):
        process_pendaftaran.validate_name(data.name)
        process_pendaftaran.validate_phone(data.phone)
        process_pendaftaran.validate_email(data.email)
````
## 4. Fungsi main
Fungsi utama main() mengendalikan alur program. Di dalamnya, program akan terus meminta input dari pengguna dan memvalidasi data hingga pengguna memilih untuk berhenti.

```python
Copy code
import re
from Data.Data1 import Data_Pendaftaran
from View.View1 import view_pendaftaran
from Process.Process1 import process_pendaftaran

def main():
    data_table = []
    while True:
        try:
            name, phone, email = view_pendaftaran.get_input()
            data = Data_Pendaftaran(name, phone, email)
            
            process_pendaftaran.validate_data(data)
            
            data_table.append(data)
            view_pendaftaran.display_message("pendaftaran valid")
            
            view_pendaftaran.table_view(data_table)
        except ValueError as e:
            view_pendaftaran.display_message(f"Error: {e}")
            
        continue_input = input("apakah anda ingin melalukan pendaftaran lagi? (y/n): ")
        if continue_input.lower() != "y":
            break
    
if __name__=="__main__":
    main()
```

## 5. Menjalankan Program
Program dijalankan dengan memanggil fungsi main(). Setiap kali pengguna memasukkan data, program akan memvalidasi data tersebut, kemudian menambahkannya ke dalam tabel jika data valid.
