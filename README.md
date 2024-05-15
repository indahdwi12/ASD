# Definisikan struktur data (tetap sama)
class MataKuliah:
    def __init__(self, kode_matkul, nama_matkul, sks, dosen, hari, jam_mulai, jam_selesai, ruang, kebutuhan_ruang):
        self.kode_matkul = kode_matkul
        self.nama_matkul = nama_matkul
        self.sks = sks
        self.dosen = dosen
        self.hari = hari
        self.jam_mulai = jam_mulai
        self.jam_selesai = jam_selesai
        self.ruang = ruang
        self.kebutuhan_ruang = kebutuhan_ruang

class Dosen:
    def __init__(self, NIP, nama, matkul_diampu):
        self.NIP = NIP
        self.nama = nama
        self.matkul_diampu = matkul_diampu

class RuangKelas:
    def __init__(self, kode_ruang, kapasitas, ketersediaan):
        self.kode_ruang = kode_ruang
        self.kapasitas = kapasitas
        self.ketersediaan = ketersediaan

# Data sampel (ganti dengan data asli Anda)
matkul_list = [
    MataKuliah("AA11", "Algoritma & Struktur Data", 3, "Dosen A", "Senin", "08:00", "09:30", "R101", 30),
    MataKuliah("BB22", "Statistika", 2, "Dosen B", "Selasa", "10:00", "11:30", "R202", 20),
    MataKuliah("CC33", "Database Managemen System", 3, "Dosen C", "Rabu", "13:00", "14:30", "R303", 30),
    MataKuliah("DD44", "Sistem Operasi", 3, "Dosen D", "Kamis", "15:00", "16:30", "R404", 40),
    MataKuliah("EE55", "Arsitektur", 2, "Dosen E", "Jumat", "17:00", "18:30", "R505", 25)
]

dosen_list = [
    Dosen("D001", "Dosen A", ["IF101"]),
    Dosen("D002", "Dosen B", ["MTK102"]),
    Dosen("D003", "Dosen C", ["IF203"]),
    Dosen("D004", "Dosen D", ["SI104"]),
    Dosen("D005", "Dosen E", ["IF305"])
]

ruang_list = [
    RuangKelas("R101", 30, True),
    RuangKelas("R202", 25, True),
    RuangKelas("R303", 35, True),
    RuangKelas("R404", 40, True),
    RuangKelas("R505", 20, True)
]

def cari_matkul():
    keyword = input("Masukkan kata kunci pencarian: ")
    hasil_cari = []
    
    # Cari berdasarkan kode mata kuliah
    hasil_cari.extend([matkul for matkul in matkul_list if keyword.lower() in matkul.kode_matkul.lower()])
    
    # Cari berdasarkan nama mata kuliah
    hasil_cari.extend([matkul for matkul in matkul_list if keyword.lower() in matkul.nama_matkul.lower()])

    # Hapus duplikat
    hasil_cari = list(set(hasil_cari))

    if hasil_cari:
        print("\nHasil Pencarian:")
        for i, matkul in enumerate(hasil_cari):
            print(f"{i+1}. {matkul.kode_matkul} - {matkul.nama_matkul}")
    else:
        print("Mata kuliah tidak ditemukan.")

# Fungsi Menu Utama
def main_menu():
    while True:
        print("\nMenu Utama:")
        print("1. Tampilkan Daftar Mata Kuliah")
        print("2. Tambah Mata Kuliah Baru")
        print("3. Hapus Mata Kuliah")
        print("4. Cari Mata Kuliah")
        print("5. Keluar")

        choice = input("Masukkan pilihan Anda (1-6): ")

        if choice == '1':
            tampilkan_daftar_matkul()
        elif choice == '2':
            tambah_matkul()
        elif choice == '3':
            hapus_matkul()
        elif choice == '4':
            cari_matkul()
        elif choice == '5':
            print("Program selesai.")
            exit()
        else:
            print("Pilihan tidak valid. Silahkan masukkan angka 1-6.")

# Fungsi untuk menampilkan daftar mata kuliah 
def tampilkan_daftar_matkul():
    if not matkul_list:
        print("Daftar mata kuliah kosong.")
        return

    print("\nDaftar Mata Kuliah:")
    for i, matkul in enumerate(matkul_list):
        print(f"{i+1}. {matkul.kode_matkul} - {matkul.nama_matkul}")

# Fungsi untuk menambahkan mata kuliah baru
def tambah_matkul():
    kode_matkul = input("Masukkan kode mata kuliah: ")
    nama_matkul = input("Masukkan nama mata kuliah: ")
    sks = int(input("Masukkan SKS: "))
    dosen = input("Masukkan nama dosen: ")
    hari = input("Masukkan hari (Senin, Selasa, Rabu, Kamis, Jumat): ")
    jam_mulai = input("Masukkan jam mulai (format HH:MM): ")
    jam_selesai = input("Masukkan jam selesai (format HH:MM): ")
    ruang = input("Masukkan ruang kelas: ")
    kebutuhan_ruang = int(input("Berapa ruang kelas yang dibutuhkan? : "))

    new_matkul = MataKuliah(kode_matkul, nama_matkul, sks, dosen, hari, jam_mulai, jam_selesai, ruang, kebutuhan_ruang)
    matkul_list.append(new_matkul)
    print("Mata kuliah baru berhasil ditambahkan.")

# Fungsi untuk menghapus mata kuliah
def hapus_matkul():
    if not matkul_list:
        print("Daftar mata kuliah kosong.")
        return

    tampilkan_daftar_matkul()
    index_hapus = int(input("Masukkan nomor mata kuliah yang ingin dihapus: ")) - 1

    if 0 <= index_hapus < len(matkul_list):
        del matkul_list[index_hapus]
        print("Mata kuliah berhasil dihapus.")
    else:
        print("Nomor mata kuliah tidak valid.")

if __name__ == "__main__":
    main_menu()
