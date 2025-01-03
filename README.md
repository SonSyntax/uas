# uas

Program ini terdiri dari beberapa kelas utama, yaitu Data, view, dan process.

1. Kelas Data
Kelas Data digunakan untuk menyimpan informasi pengguna yang terdiri dari Nama, No. Telp, dan Email.

```python
Copy code
class Data:
    def __init__(self, name, phone, email):
        self.name = name
        self.phone = phone
        self.email = email
````

2. Kelas view
Kelas view bertanggung jawab untuk menangani tampilan dan interaksi dengan pengguna. Kelas ini memiliki beberapa metode:

get_input(): Untuk meminta input dari pengguna (Nama, No. Telp, dan Email).
table_view(data_table): Untuk menampilkan tabel yang berisi data pengguna yang sudah terdaftar.
display_message(message): Untuk menampilkan pesan kepada pengguna.
```python
Copy code
class view:
    @staticmethod
    def get_input():
        name = input("Nama: ")
        phone = input("No. Telp: ")
        email = input("Email: ")
        return name, phone, email
    
    @staticmethod
    def table_view(data_table):
        print("="*93)
        print("| NO |               NAMA               |        NO.TELP        |           EMAIL           |")
        print("="*93)
        
        for i, data in enumerate(data_table, start=1):
            print(f"| {i:<2} | {data.name:<32} | {data.phone:<21} | {data.email:<25} |")
        print("="*93)
        
    @staticmethod
    def display_message(message):
        print(message)
````

3. Kelas process
Kelas process berfungsi untuk memvalidasi data yang dimasukkan oleh pengguna. Metode-metode dalam kelas ini adalah:

validate_name(name): Memastikan nama hanya berisi huruf.
validate_phone(phone): Memastikan nomor telepon hanya berisi angka.
validate_email(email): Memastikan email mengikuti format yang benar.
validate_data(data): Menggabungkan semua validasi menjadi satu fungsi untuk memvalidasi seluruh data.

```python
Copy code
class process:
    @staticmethod
    def validate_name(name):
        if not name.isalpha():
            raise ValueError("Hanya berisi huruf")
        
    @staticmethod
    def validate_phone(phone):
        if not phone.isdigit():
            raise ValueError("hanya berisi angka")
        
    @staticmethod
    def validate_email(email):
        if not re.match(r"[^@]+@[^@]+\.[^@]+", email):
            raise ValueError("harus meggunakan huruf '@' & '.'  .")
        
    @staticmethod
    def validate_data(data):
        process.validate_name(data.name)
        process.validate_phone(data.phone)
        process.validate_email(data.email)
````
4. Fungsi main
Fungsi utama main() mengendalikan alur program. Di dalamnya, program akan terus meminta input dari pengguna dan memvalidasi data hingga pengguna memilih untuk berhenti.

```python
Copy code
def main():
    data_table = []
    while True:
        try:
            name, phone, email = view.get_input()
            data = Data(name, phone, email)
            
            process.validate_data(data)
            
            data_table.append(data)
            view.display_message("pendaftaran valid")
            
            view.table_view(data_table)
        except ValueError as e:
            view.display_message(f"Error: {e}")
            
        continue_input = input("apakah anda ingin melalukan pendaftaran lagi? (y/n): ")
        if continue_input.lower() != "y":
            break
```

5. Menjalankan Program
Program dijalankan dengan memanggil fungsi main(). Setiap kali pengguna memasukkan data, program akan memvalidasi data tersebut, kemudian menambahkannya ke dalam tabel jika data valid.
