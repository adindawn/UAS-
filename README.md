# PROJECT UAS BAHASA PEMROGRAMAN 

NAMA  : ADINDA AULIA NABILA PUTRI

NIM   : 312410309

KELAS : TI.24.A.4 


![WhatsApp Image 2025-01-05 at 14 31 03_f49fbe9e](https://github.com/user-attachments/assets/862dfee8-c230-4ac6-9a50-dc4c934d534a)

Program ini adalah aplikasi sederhana untuk sistem peminjaman buku berbasis terminal. Program ini dibuat dengan pendekatan modular dan menggunakan prinsip OOP (Object-Oriented Programming). Program memungkinkan pengguna untuk melihat daftar buku, memasukkan data peminjaman, dan menampilkan detail peminjaman dengan validasi input. 


```PYTHON
# Class Data
class BookData:
    def _init_(self):
        self.books = [
            {"id": 1, "title": "Python Programming", "available": True},
            {"id": 2, "title": "Data Science 101", "available": True},
            {"id": 3, "title": "Machine Learning Basics", "available": True},
        ]
        self.bookings = []

    def get_available_books(self):
        return [book for book in self.books if book["available"]]

    def book_a_book(self, book_id, name, days):
        for book in self.books:
            if book["id"] == book_id and book["available"]:
                book["available"] = False
                self.bookings.append({"name": name, "title": book["title"], "days": days})
                return True
        return False

# Class View
class BookView:
    def display_books(books):
        print("\nAvailable Books:")
        if books:
            print("ID | Title")
            print("---|------------------------")
            for book in books:
                print(f"{book['id']}  | {book['title']}")
        else:
            print("No books available at the moment.")

    def display_bookings(bookings):
        print("\nCurrent Bookings:")
        if bookings:
            print("Name         | Book Title              | Days")
            print("-------------|-------------------------|------")
            for booking in bookings:
                print(f"{booking['name']:<12} | {booking['title']:<23} | {booking['days']}")
        else:
            print("No bookings made yet.")

    def input_message(message):
        return input(message)

    def error_message(message):
        print(f"Error: {message}")

    def success_message(message):
        print(f"Success: {message}")

# Class Process
class BookProcess:
    def _init_(self, data, view):
        self.data = data
        self.view = view

    def run(self):
        while True:
            print("\n1. View available books")
            print("2. Book a book")
            print("3. View current bookings")
            print("4. Exit")
            choice = self.view.input_message("Choose an option (1-4): ")

            if choice == "1":
                available_books = self.data.get_available_books()
                self.view.display_books(available_books)

            elif choice == "2":
                available_books = self.data.get_available_books()
                self.view.display_books(available_books)
                try:
                    book_id = int(self.view.input_message("Enter the Book ID to book: "))
                    name = self.view.input_message("Enter your name: ")
                    days = int(self.view.input_message("Enter number of days for booking (1-30): "))

                    if days < 1 or days > 30:
                        raise ValueError("Booking days must be between 1 and 30.")

                    if self.data.book_a_book(book_id, name, days):
                        self.view.success_message("Book successfully booked!")
                    else:
                        self.view.error_message("Book is not available or invalid ID.")
                except ValueError as e:
                    self.view.error_message(str(e))

            elif choice == "3":
                self.view.display_bookings(self.data.bookings)

            elif choice == "4":
                print("Exiting the program. Goodbye!")
                break

            else:
                self.view.error_message("Invalid option. Please choose again.")

# Main Program
def main():
    data = BookData()
    view = BookView()
    process = BookProcess(data, view)
    process.run()

if __name__ == "_main_":
    main()
````

# CLASS DATA 

```PYTHON
# Class Data
class BookData:
    def __init__(self):
        self.books = [
            {"id": 1, "title": "Python Programming", "available": True},
            {"id": 2, "title": "Data Science 101", "available": True},
            {"id": 3, "title": "Machine Learning Basics", "available": True},
        ]
        self.bookings = []
````

Class Books Data untuk menyimpan dan mengelola data buku serta data peminjaman. books untuk
menyimpan data buku dalam bentuk list, setiap buku memiliki id, title, dan status available dan Bookings untuk menyimpan daftar peminjaman yang dilakukan, termasuk nama peminjam, judul buku, dan jumlah hari peminjaman.


```PYTHON
 def get_available_books(self):
        return [book for book in self.books if book["available"]]
````

def get_available_books(self), mengembalikan daftar buku yang masih tersedia untuk dipinjam dan untuk menampilkan buku-buku yang statusnya available=true.


```PYTHON
def book_a_book(self, book_id, name, days):
        for book in self.books:
            if book["id"] == book_id and book["available"]:
                book["available"] = False
                self.bookings.append({"name": name, "title": book["title"], "days": days})
                return True
        return False
````

Memproses peminjaman buku berdasarkan ID yang diberikan. Jika buku tersedia, statusnya diubah menjadi tidak tersedia dan data peminjaman ditambah ke bookings. Jika peminjaman berhasil maka rograman akan menampilkan True dan jika peminjaman tidak berhasil maka program akan menampilkan false.


# Class View 

```PYTHON
# Class View
class BookView:
    def display_books(books):
        print("\nAvailable Books:")
        if books:
            print("ID | Title")
            print("---|------------------------")
            for book in books:
                print(f"{book['id']}  | {book['title']}")
        else:
            print("No books available at the moment.")

    def display_bookings(bookings):
        print("\nCurrent Bookings:")
        if bookings:
            print("Name         | Book Title              | Days")
            print("-------------|-------------------------|------")
            for booking in bookings:
                print(f"{booking['name']:<12} | {booking['title']:<23} | {booking['days']}")
        else:
            print("No bookings made yet.")

    def input_message(message):
        return input(message)

    def error_message(message):
        print(f"Error: {message}")

   def success_message(message):
        print(f"Success: {message}")
````

Class Book View, menangani interaksi dengan pengguna, termasuk menampilkan informasi dan menerimaa input. Display_books, untuk menampilkan daftra yang tersedia dalam format tabel. Display bookings, untuk menampilkan daftra peminjaman dalam format tabel. Input_message, Meminta input dari pengguna dengan pesan prompt tertentu. Error_message, Menampilkan pesan kesalahan kepada pengguna jika terjadi error. Dan Method Success_message, program akan menampilkan pesan "SUCCESS" jika berhasil meminjam buku. 


# Class Process

```PYTHON
# Class Process
class BookProcess:
    def __init__(self, data, view):
        self.data = data
        self.view = view
````

Class Book Process, untuk mengelola logika utama dari program dan menghubungkan bookdata dan bookview
    
    * Data = Mengacu ke objek Bookdata untuk mendapatkan inforamsi tentang buku dan peminjaman. 
    
    * View = Mengacu ke objek Bookview untuk menampilkan informasi kepada pengguna. 


```PYTHON
def run(self):
        while True:
            print("\n1. View available books")
            print("2. Book a book")
            print("3. View current bookings")
            print("4. Exit")
            choice = self.view.input_message("Choose an option (1-4): ")

            if choice == "1":
                available_books = self.data.get_available_books()
                self.view.display_books(available_books)

            elif choice == "2":
                available_books = self.data.get_available_books()
                self.view.display_books(available_books)
                try:
                    book_id = int(self.view.input_message("Enter the Book ID to book: "))
                    name = self.view.input_message("Enter your name: ")
                    days = int(self.view.input_message("Enter number of days for booking (1-30): "))

                    if days < 1 or days > 30:
                        raise ValueError("Booking days must be between 1 and 30.")

                    if self.data.book_a_book(book_id, name, days):
                        self.view.success_message("Book successfully booked!")
                    else:
                        self.view.error_message("Book is not available or invalid ID.")
                except ValueError as e:
                    self.view.error_message(str(e))

            elif choice == "3":
                self.view.display_bookings(self.data.bookings)

            elif choice == "4":
                print("Exiting the program. Goodbye!")
                break

            else:
                self.view.error_message("Invalid option. Please choose again.")
````

Method Run, menyediakan menu utama interaktif bagi pengguna serta memiliki 4 opsi menu : 
  1. Menampilkan daftar buku yang teesedia
  2. Memproses peminjaman buku :

     * Meminta ID buku, Nama peminjaman, dan Jumlah hari peminjaman.

     * Memvalidasi input (jumlah hari harus diantar 1-30).

     * Mengubah status buku menjadi tidak tersedia jika peminjaman berhasil.
  4. Menampilka daftar buku peminjaman yang telah dilakukan.
  5. Keluar dari program.



# Main Program 

```PYTHON
# Main Program
def main():
    data = BookData()
    view = BookView()
    process = BookProcess(data, view)
    process.run()

if __name__ == "__main__":
    main()
````

Fungsi main: 
  1. Membuat objek BookData, BookView, dan BookProcess.
  2. Menjalankan Method Run dari BookProcess untuk memulai program. 



Berikut Hasil Outputnya 

![Screenshot 2025-01-07 154431](https://github.com/user-attachments/assets/131460ee-8c6a-4660-94ab-9efef809f105)

![Screenshot 2025-01-07 154445](https://github.com/user-attachments/assets/513c9eea-32f0-4bd0-b606-1c90f694cf7a)











