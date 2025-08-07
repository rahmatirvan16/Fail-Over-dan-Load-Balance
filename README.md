## Konsep Fail Over & Load Balance
  <br>Fail Over adalah Settingan Mikrotik dengan Setingan 1 Aktif dan 1 Backup
  <br>Load Balance adalah Setingan Mikrotik dengan kedua ISP Aktif (sebgaian ke ISP Pertama dan sebagian ke ISP Kedua)
## Konfigurasi Fail Over
## Check Gateway
  <br>Fitur untuk setting automasi ISP lebih dari 1 ke ISP aktif, jika saat ping menghasilkan time out
  ```
  ip route set 0 check-gateway=ping
  ``` 
## Load Balance ECMP
  <br>Pembagian paket/jalur koneksi internet secara acak dan tidak bisa ditentukan
  <br>Settingan routing (1 dst-address dan beberapa gateway) dengan pembagian routing sama rata
  <br>
  <br>cara hapus gateway lebih dari satu
  ```
  ip route remove 0,1
  ```
  cara menambahkan gateway lebih dari satu
  ```
  ip route add gateway=192.168.111.1,192.168.122.1
  ```
  Jika salah satu gateway penggunaannya ingin lebih besar atau 2x maka rubah dengan langkah berikut
  ```
  ip route set 0 gateway=192.168.122.1,192.168.111.1,192.168.111.1
  ```
  maka 192.168.111.1 penggunaan gateway 2x lebih banyak dari pada 192.168.111.1
   <br>
## Load Balance Routing Mark (Route Rules)
  <br> Pembagian paket/jalur koneksi internet secara teratur terhadap client/pc yang ditentukan
  <br>Load Balance Routing Mark adalah Pengarahan/Pembagian routing ke beberapa ISP sesuai dengan setingan yang telah ditentukan
  <br> Cara membuat rule
  ```
  ip route rule add src-address=192.168.1.254 table=pc1
  ```
    ```
  ip route rule add src-address=192.168.1.253 table=pc2
  ```
  Tampilan routing rule di Winbox
  <img width="800" height="243" alt="Image" src="https://github.com/user-attachments/assets/f59e1d73-ecc8-48cf-8204-cfd9c57a4856" />
  <br> Cara membuat routing mark Ke ISP1 dan ISP2
  ```
  ip route add dst-address=0.0.0.0/0 gateway=192.168.111.1 routing-mark=pc1
  ```
    ```
  ip route add dst-address=0.0.0.0/0 gateway=192.168.122.1 routing-mark=pc2
  ```
  <br> Tampilan routing mark di Winbox
  <img width="800" height="356" alt="Image" src="https://github.com/user-attachments/assets/32b62c51-0481-4ba0-bd4f-dc09100ec54e" />
## Konsep Main Routing
  <br> Tampilan di CLI
  <br>
  <img width="800" height="205" alt="Image" src="https://github.com/user-attachments/assets/e0bad57e-816a-4077-b36a-f35c3862e084" />
  <br> Cara rubah gateway di baris ke 2
  ```
  ip route set 2 gateway=192.168.122.1
  ```
  Cara enable route di baris ke 2
  ```
  ip route enable 2
  ```
## Load Balance Routing Mark (Firewall Mangle)
  <br> Pembagian jalur paket/koneksi menggunakan firewal mangle
  <br> langkah-langkahnya IP->Firewall->Manggle
<br>General
  - Chain = prerouting
  - src address = 192.168.1.254
  <br>Action
  - Action = mark routing
  - New Routing Mark = mangle_pc1
<br>Tampilan di Winbox
<img width="800" height="234" alt="Image" src="https://github.com/user-attachments/assets/ea5364df-d8f4-42f7-aa07-0e2bf37b260c" />

**Kelebihan** Firewall Mangle dibandingkan Routes Rules adalah bisa menandai paket berdasarkan protokol, misalnya https lewat ISP1 dan http ke ISP2 atau email lewat ISP1 youtube lewat ISP2
<br> kemudian setting route IP->route
- Dst address = 0.0.0.0
- Gateway = 192.168.111.1
- Routing Mark = mangle_pc1
<br>Tampilan Winbox
<br>
<img width="800" height="325" alt="Image" src="https://github.com/user-attachments/assets/14b08edf-e536-4c89-8e6d-0680b671123f" />

## Address List untuk Mangle
<br> Mengelompokkan IP
<br>Pertama Setting Address List untuk melakukan pengelompokkan IP

* name : via_isp1
* address : 192.168.1.2-192.168.1.100
<img width="800" height="267" alt="Image" src="https://github.com/user-attachments/assets/e20f9b90-f5c6-4680-a2b3-afd99a16f36f" />
<br>Kedua Setting Mangle dengan src. address list yang sesuai dengan address list dibuat

* chain = prerouting
* src. address list = via_isp1
* action = mark routing
* new routing mark = ISP1
<img width="800" height="264" alt="Image" src="https://github.com/user-attachments/assets/f245e437-12b6-4b23-8222-8fef436e0a97" />
<br>Ketiga Setting Routing dengan Routing Mark sesuai Mangle

* dst. address = 0.0.0.0/24
* gateway = 192.168.111.1
* routing mark = ISP1
<img width="800" height="329" alt="image" src="https://github.com/user-attachments/assets/a114ab95-5486-4585-9cf1-b9d6ec9c9374" />

