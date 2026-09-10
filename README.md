# PBKK C - P2
Tugas PBKK C pertemuan ke-2  
Al Jad Kaukabudduri Hardianto 5025241248

1. Struktur data
```
namespace DataMahasiswa
{
    class Mahasiswa
    {
        public string NIM { get; set; }
        public string Nama { get; set; }
        public string Prodi { get; set; }
        public double IPK { get; set; }

        public Mahasiswa(string nim, string nama, string prodi, double ipk)
        {
            NIM = nim;
            Nama = nama;
            Prodi = prodi;
            IPK = ipk;
        }
    }

    class Program
    {
        static List<Mahasiswa> daftarMahasiswa = new List<Mahasiswa>();
    }
}
```
`namespace DataMahasiswa` adalah wadah untuk mengelompokkan class yang berkaitan dengan aplikasi data mahasiswa.
`class Mahasiswa` adalah cetakan/template untuk satu data mahasiswa.
`NIM, Nama, Prodi, dan IPK` adalah properti yang dimiliki setiap mahasiswa.
`daftarMahasiswa` adalah list yang menyimpan semua objek mahasiswa.
`static` membuat `daftarMahasiswa` bisa dipakai langsung oleh method lain dalam class Program.

2. Tampilan menu
```
static void TampilkanMenu()
{
    Console.Clear();

    Console.WriteLine("========================================");
    Console.WriteLine(" SISTEM DATA MAHASISWA");
    Console.WriteLine("========================================");
    Console.WriteLine("1. Tambah Mahasiswa");
    Console.WriteLine("2. Tampilkan Mahasiswa");
    Console.WriteLine("3. Cari Mahasiswa");
    Console.WriteLine("4. Hapus Mahasiswa");
    Console.WriteLine("5. Keluar");
    Console.WriteLine("========================================");
}
```
`static void TampilkanMenu()` adalah method untuk menampilkan menu utama.
`Console.Clear()` membersihkan tampilan console sebelum menu ditampilkan lagi.
`Console.WriteLine()` menampilkan teks lalu pindah ke baris berikutnya.
Dokumentasi: 
<img width="375" height="222" alt="Screenshot 2026-09-10 152918" src="https://github.com/user-attachments/assets/adde012b-8de1-435c-afb7-735e87ee59a8" />

3. Fitur tambah mahasiswa
```
static void TambahMahasiswa()
{
    Console.Clear();

    Console.WriteLine("========================================");
    Console.WriteLine(" TAMBAH MAHASISWA");
    Console.WriteLine("========================================");

    Console.Write("NIM : ");
    string nim = Console.ReadLine();

    Console.Write("Nama : ");
    string nama = Console.ReadLine();

    Console.Write("Program Studi : ");
    string prodi = Console.ReadLine();

    double ipk;

    while (true)
    {
        Console.Write("IPK : ");

        if (double.TryParse(Console.ReadLine(), out ipk))
        {
            if (ipk >= 0 && ipk <= 4)
            {
                break;
            }
        }

        Console.WriteLine("IPK harus berupa angka 0 - 4.");
    }

    Mahasiswa mahasiswa = new Mahasiswa(nim, nama, prodi, ipk);
    daftarMahasiswa.Add(mahasiswa);

    Console.WriteLine();
    Console.WriteLine("Data mahasiswa berhasil ditambahkan.");
}
```
`Console.Clear()` membersihkan menu utama agar pengguna fokus pada halaman input.
`Console.Write()` meminta pengguna memasukkan NIM, nama, dan program studi.
`while (true)` membuat program terus meminta IPK sampai input valid.
`double.TryParse(...)` memastikan bahwa input IPK benar-benar angka desimal.
`ipk >= 0 && ipk <= 4` Jika valid, `break` menghentikan perulangan. Jika salah, akan menampilkan pesan "IPK harus berupa angka 0 - 4."
Dokumentasi:
<img width="381" height="281" alt="Screenshot 2026-09-10 152811" src="https://github.com/user-attachments/assets/5ba2ec00-4d4a-40c2-a324-ab846c7cf855" />

4. Fitur list mahasiswa
```
static void TampilkanMahasiswa()
{
    Console.Clear();

    Console.WriteLine("==========================================================");
    Console.WriteLine(" DAFTAR MAHASISWA");
    Console.WriteLine("==========================================================");

    if (daftarMahasiswa.Count == 0)
    {
        Console.WriteLine("Belum ada data mahasiswa.");
        return;
    }

    Console.WriteLine(
        "{0,-12} {1,-20} {2,-20} {3,5}",
        "NIM",
        "Nama",
        "Prodi",
        "IPK"
    );

    Console.WriteLine("----------------------------------------------------------");

    foreach (Mahasiswa m in daftarMahasiswa)
    {
        Console.WriteLine(
            "{0,-12} {1,-20} {2,-20} {3,5:F2}",
            m.NIM,
            m.Nama,
            m.Prodi,
            m.IPK
        );
    }

    Console.WriteLine("==========================================================");
}
```
`daftarMahasiswa.Count` menghitung jumlah data mahasiswa dalam list.
Jika jumlah datanya 0 akan mengeluarkan pesan "Belum ada data mahasiswa."
Dokumentasi:
<img width="660" height="221" alt="Screenshot 2026-09-10 152838" src="https://github.com/user-attachments/assets/f962ec89-8038-4fa8-90c7-8bd2b32627d3" />

5. Fitur cari mahasiswa
```
static void CariMahasiswa()
{
    Console.Clear();

    Console.WriteLine("========================================");
    Console.WriteLine(" CARI MAHASISWA");
    Console.WriteLine("========================================");

    Console.Write("Masukkan NIM: ");
    string nimCari = Console.ReadLine();

    Mahasiswa mahasiswaDitemukan = null;

    foreach (Mahasiswa m in daftarMahasiswa)
    {
        if (m.NIM.Equals(nimCari, StringComparison.OrdinalIgnoreCase))
        {
            mahasiswaDitemukan = m;
            break;
        }
    }

    Console.WriteLine();

    if (mahasiswaDitemukan != null)
    {
        Console.WriteLine("Data ditemukan!");
        Console.WriteLine("NIM : " + mahasiswaDitemukan.NIM);
        Console.WriteLine("Nama : " + mahasiswaDitemukan.Nama);
        Console.WriteLine("Prodi : " + mahasiswaDitemukan.Prodi);
        Console.WriteLine("IPK : " + mahasiswaDitemukan.IPK.ToString("F2"));
    }
    else
    {
        Console.WriteLine("Mahasiswa dengan NIM tersebut tidak ditemukan.");
    }
}
```
`nimCari` menyimpan NIM dari pengguna.
`foreach` memeriksa seluruh mahasiswa yang tersimpan di daftarMahasiswa.
`StringComparison.OrdinalIgnoreCase` berarti perbandingan tidak membedakan huruf besar dan kecil.
Jika `mahasiswaDitemukan != null`, program menampilkan seluruh data mahasiswa.
Dokumentasi:
<img width="371" height="288" alt="Screenshot 2026-09-10 152852" src="https://github.com/user-attachments/assets/205461ba-8833-4f78-9bca-d223088d41cd" />

6. Fitur hapus mahasiswa
```
static void HapusMahasiswa()
{
    Console.Clear();

    Console.WriteLine("========================================");
    Console.WriteLine(" HAPUS MAHASISWA");
    Console.WriteLine("========================================");

    Console.Write("Masukkan NIM: ");
    string nimHapus = Console.ReadLine();

    Mahasiswa mahasiswaDitemukan = null;

    foreach (Mahasiswa m in daftarMahasiswa)
    {
        if (m.NIM.Equals(nimHapus, StringComparison.OrdinalIgnoreCase))
        {
            mahasiswaDitemukan = m;
            break;
        }
    }

    if (mahasiswaDitemukan != null)
    {
        daftarMahasiswa.Remove(mahasiswaDitemukan);

        Console.WriteLine();
        Console.WriteLine("Data mahasiswa berhasil dihapus.");
    }
    else
    {
        Console.WriteLine();
        Console.WriteLine("Data mahasiswa tidak ditemukan.");
    }
}
```
`nimHapus` menyimpan NIM input pengguna.
Program melakukan pencarian seperti pada fitur cari mahasiswa
`Remove()` menghapus objek mahasiswa tersebut dari daftarMahasiswa.
Dokumentasi:
<img width="372" height="200" alt="Screenshot 2026-09-10 152907" src="https://github.com/user-attachments/assets/1c4829db-bdc4-4f97-9350-79c4352c2028" />

7. Fitur keluar
```
case 5:
    Console.WriteLine("Terima kasih telah menggunakan program.");
    break;
```
Dokumentasi:
<img width="377" height="292" alt="Screenshot 2026-09-10 152927" src="https://github.com/user-attachments/assets/60e21856-8fb7-4c3e-8378-395fed9c5275" />
