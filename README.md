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

## Diagram Basis Data

```mermaid
Table users {
  id int [pk, increment] // Primary Key
  name varchar
  email varchar [unique]
  password varchar
  role varchar // 'guru' atau 'siswa'
  created_at timestamp
}

Table admins {
  id int [pk, increment] // Primary Key
  name varchar
  email varchar [unique]
  password varchar
  created_at timestamp
}

Table facilities {
  id int [pk, increment]
  name varchar
  description text
  type varchar // 'fasilitas' atau 'ruangan'
  capacity int
  created_at timestamp
}
Table ruangan {
  id int [pk, increment]
  name varchar
  description text
  type varchar // 'fasilitas' atau 'ruangan'
  capacity int
  created_at timestamp
}

Table bookings {
  id int [pk, increment]
  user_id int [ref: > users.id]
  facility_id int [ref: > facilities.id]
  ruangan_id int [ref: > ruangan.id]
  booking_date date
  start_time time
  end_time time
  status varchar // pending, approved, rejected
  created_at timestamp
}


Table penyetujuan_booking {
  id int [pk, increment]
  booking_id int [ref: > bookings.id]
  admin_id int [ref: > admins.id]
  waktu_penyetujuan timestamp
  status varchar // approved, rejected
  notes text
}

