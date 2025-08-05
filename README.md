- **Konsep Fail Over & Load Balance**
  <br>Fail Over adalah Settingan Mikrotik dengan Setingan 1 Aktif dan 1 Backup
  <br>Load Balance adalah Setingan Mikrotik dengan kedua ISP Aktif (sebgaian ke ISP Pertama dan sebagian ke ISP Kedua)
- **Konfigurasi Fail Over**
- **Check Gateway**
  <br>Fitur untuk setting automasi ISP lebih dari 1 ke ISP aktif, jika saat ping menghasilkan time out
  ```
  ip route set 0 check-gateway=ping
  ``` 
- **Load Balance ECMP**
  <br>Settingan routing (1 dst-address dan beberapa gateway) dengan pembagian routing sama rata
  cara hapus gateway lebih dari satu
  ```
  ip route remove 0,1
  ```
  cara menambahkan gateway lebih dari satu
  ```
  ip route add gateway=192.168.111.1,192.168.122.1
  ```
  Jika salah satu gateway penggunaannya lebih besar maka rubah dengan langkah berikut
  ```
  ip route set 0 gateway=192.168.122.1,192.168.111.1,192.168.111.1
  ```
  maka 192.168.111.1 penggunaan gateway 2x lebih banyak dari pada 192.168.111.1
   <br>
- **Load Balance Routing Mark (Route Rules)**
  Berbeda dangan load balance ECMP yang pembagian paket secara acak,
  <br>Load Balance Routing Mark adalah Pengarahan/Pembagian routing ke beberapa ISI sesuai dengan setingan yang telah ditentukan
  <br> La
  ```
  ip route set 0 gateway=192.168.122.1,192.168.111.1,192.168.111.1
  ```
  
- **Konsep Main Routing**
- **Load Balance Routing Mark (Firewall Mangle)**
- **Address List untuk Mangle**
