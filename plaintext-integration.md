# Documentation Plaintext Integration

# Daftar Isi

1. [General Description](#general-description)
2. [Revision History](#revision-history)
3. [API Service](#api-service)
  
    3.1. [Transactions](#transactions)
    
    - [Request Transactions](#request-transactions)
    - [Response Transactions](#response-transactions)
    - [Response Saldo Tidak Cukup](#response-saldo-tidak-cukup)
    
    3.2. [Balance](#balance)
    
    - [Request Balance](#request-balance)
    - [Response Balance](#response-balance)
    
    3.3. [Ticket](#request-ticket)
    - [Request Ticket](#request-ticket)
    - [Response Ticket](#response-ticket)
4. [Callback Format](#callback-format)  
    4.1. [Example Callback](#example-callback)
5. [Response Code](#response-code)
6. [Lisensi](#lisensi)
    

# General Description

Spesifikasi ini merincikan API yang memungkinkan pengguna untuk menjalankan bisnis penjualan pulsa dan layanan pembayaran tagihan (PPOB) secara online. Dengan API ini, pengguna dapat melakukan berbagai operasi, termasuk menjual pulsa, melakukan pembayaran tagihan listrik, air, internet, dan banyak lagi. API ini dirancang untuk memudahkan proses bisnis penjualan pulsa dan layanan PPOB bagi pedagang dan memberikan akses yang aman dan efisien kepada penyedia layanan.

# Revision History

| Doc Version | Release Platform Version | Date Modified | Created By | Modified By | Description |
| --- | --- | --- | --- | --- | --- |
| 2.0 | V2.0 | 10/09/2023 | Agus Novian |  | Initial V2.0 |
| 2.0 | V2.1 | 14/09/2023 |  | Agus Novian | Revisi RC V2.0 |

# API Service

## Transactions

- _**Request Transactions**_
    
    ``` http
    GET /trx?product={T10}}&dest={08xxxxx}&refID={20240123}&memberID={memberID}&pin={pin}&password={password}
    
     ```
    
- _**Response Transactions**_
    
    ``` http
    HTTP/1.1 200 OK
    #130454449 R#20240123 T10.08xxxxx akan diproses @08.04. Saldo 10.345 - 0 = 10.345 kode_reseller={memberID} TRX Normal
    
     ```
    
- _**Response Saldo Tidak Cukup**_
    
    ``` http
    HTTP/1.1 200 OK
    R#130454449'R#20240123 TEST123.08...' GAGAL. Saldo tidak cukup.08xxxxx Hrg 1xx.xxx, Saldo 66.616 Limit 0, proses 0. KetikTIKET utk deposit kode_reseller={memberID} TRX Normal
    
     ```
    

## Balance

- **_Request Balance**
    
    ``` http
    GET /balance?memberID={memberID}&pin={pin}&password={password}
    
     ```
    
- **_Response Balance**
    
    ``` http
    HTTP/1.1 200 OK
    Saldo Deposit Anda Rp.66.616
    {memberID} Account Test
    Pemakaian 0
    Poin 
    Trx 0
    Komisi 0 TRX Normal
    
     ```
    

## Ticket

- **_Request Ticket**
    
    ``` http
    GET /?cmd=ticket&amount=100000&memberID={memberID}&pin={pin}&password={password}
    
     ```
    
- **_Response Ticket**
    
    ``` http
    HTTP/1.1 200 OK
    Silahkan Transfer Sesuai Rp.100.697
    BCA NON FAKTUR :
    68xxxx (F Putri Nonik Arimbi) 
    BCA BERFAKTUR :
    68xxxxLTI MAKMUR INDONESIA (MANUAL Silahkan konfimasi CS)
    Tiket Deposit Close Jam 22.00 WIB
    (TIDAK TERIMA DEPOSIT VIA MESIN EDC) TRX Normal
    
     ```
    

#### Callback Format

- _**Example Callback**_
    
    ``` http
    GET https://mitra.api/callback?t=80401&refid=20230914-test&status=20&price=10345&message=#130454449 R#20230914-test TSEL10.085200001111 SUKSES. SN : 5995347047420136. Saldo Rp.20.345 - 10.345 = Rp.10.000 . @14/09 22.35.52  kode_reseller=AK21 TRX Normal
    
     ```
    

#### Response Code

| RC | Description |
| --- | --- |
| 2 | Pending |
| 20 | Sukses |
| 40 | Gagal |
| 41 | Member Not Found |
| 43 | Saldo Tidak Cukup |
| 44 | Produk Salah |
| 46 | Transaksi Dobel |
| 47 | Produk Sedang Gangguan |
| 52 | Tujuan Salah |
| 55 | Timeout |
| 57 | Invalid Signature/Invalid PIN or Password |
| 255 | Unknown |

#### Lisensi

Layanan ini dilisensikan di bawah ketentuan berikut:

##### Penggunaan Layanan

Anda diizinkan untuk menggunakan layanan ini untuk keperluan pribadi dan komersial Anda. Anda dapat mengakses dan memanfaatkan API ini sesuai dengan tujuan utamanya, yaitu mengonsumsi data dan layanan yang disediakan.

##### Pembatasan Lisensi

Dalam penggunaan layanan ini, ada beberapa pembatasan yang harus diikuti:

1. **Tidak Diizinkan untuk Merubah Kode Sumber**: Anda tidak diizinkan untuk mengubah, memodifikasi, atau menyusun ulang kode sumber atau API ini.
2. **Tidak Diizinkan untuk Mendistribusi Ulang**: Anda tidak diizinkan untuk mendistribusi ulang layanan ini kepada pihak lain tanpa izin tertulis dari pemilik lisensi.
3. **Penyalahgunaan Terhadap Layanan**: Penyalahgunaan layanan ini, seperti serangan DDoS, spam, atau penggunaan yang merugikan lainnya, dilarang dan dapat mengakibatkan penghentian akses Anda.
4. **Pemantauan Akses**: Akses Anda ke layanan ini dapat dipantau untuk tujuan keamanan dan kepatuhan.
    

##### Tanggung Jawab

Penggunaan layanan ini sepenuhnya menjadi tanggung jawab Anda. Pemilik lisensi tidak bertanggung jawab atas kerugian atau kerusakan yang timbul akibat penggunaan layanan ini.

##### Perubahan pada Lisensi

Pemilik lisensi berhak untuk mengubah ketentuan lisensi ini kapan saja tanpa pemberitahuan sebelumnya. Anda disarankan untuk memeriksa lisensi ini secara berkala.

##### Hubungi Kami

Jika Anda memiliki pertanyaan atau permintaan khusus mengenai lisensi ini, silakan hubungi kami melalui [kontak kami](https://multimakmur.id/).

Terima kasih atas pemahaman Anda dan selamat menggunakan layanan kami!
