# Framework
# Aplikasi Peminjaman Fasilitas/Ruangan Sekolah
---

## ROLE

###  Siswa
- Login ke sistem
- Melakukan peminjaman ruangan/fasilitas
- Memasukkan tanggal & durasi peminjaman
- Melihat status peminjaman (proses/disetujui/ditolak)
- Bisa melihat seluruh riwayat peminjaman pribadi
- Bisa mengedit/membatalkan peminjaman


###  Guru
- Login ke sistem
- Melakukan peminjaman ruangan/fasilitas
- Memasukkan tanggal & durasi peminjaman
- Melihat status peminjaman (proses/disetujui/ditolak)
- Bisa melihat seluruh riwayat peminjaman pribadi
- Bisa mengedit/membatalkan peminjaman

###  Admin
- Login ke sistem
- Menambah dan mengedit data ruangan/fasilitas
- Melihat semua permintaan peminjaman
- Menyetujui atau menolak permintaan peminjaman
- Mengekspor data peminjaman ke Excel 

## FITUR
- Peminjaman fasilitas sekolah online
- Role user (Admin, Guru, Siswa)
- Validasi otomatis konflik jadwal
- CRUD data barang/fasilitas
- Export data ke Excel / Power point
- Status ruangan terpinjam atau tidak

# Diagram Basis Data
```mermaid
erDiagram
    USERS {
        int id
        string name
        string email
        string password
        string role
        datetime created_at
    }

    ADMINS {
        int id
        string name
        string email
        string password
        datetime created_at
    }

    FACILITIES {
        int id
        string name
        string description
        string type
        int capacity
        datetime created_at
    }

    RUANGAN {
        int id
        string name
        string description
        string type
        int capacity
        datetime created_at
    }

    BOOKINGS {
        int id
        int user_id
        int facility_id
        int ruangan_id
        date booking_date
        time start_time
        time end_time
        string status
        datetime created_at
    }

    PENYETUJUAN_BOOKING {
        int id
        int booking_id
        int admin_id
        datetime waktu_penyetujuan
        string status
        string notes
    }

    USERS ||--o{ BOOKINGS : membuat
    FACILITIES ||--o{ BOOKINGS : digunakan
    RUANGAN ||--o{ BOOKINGS : digunakan
    ADMINS ||--o{ PENYETUJUAN_BOOKING : memproses
    BOOKINGS ||--o{ PENYETUJUAN_BOOKING : disetujui_atau_ditolak

