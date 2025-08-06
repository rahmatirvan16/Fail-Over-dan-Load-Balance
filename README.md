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
  <br>Pembagian paket secara acak
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
- **Load Balance Routing Mark (Route Rules)**
  <br> Pembagian paket secara teratur
  <br>Load Balance Routing Mark adalah Pengarahan/Pembagian routing ke beberapa ISP sesuai dengan setingan yang telah ditentukan
  <br> Cara membuat rule
  ```
  ip route rule add src-address=192.168.1.254 table=pc1
  ```
    ```
  ip route rule add src-address=192.168.1.253 table=pc2
  ```
  Tampilan routing rule di Winbox
  <img width="780" height="243" alt="Image" src="https://github.com/user-attachments/assets/f59e1d73-ecc8-48cf-8204-cfd9c57a4856" />
  <br> Cara membuat routing mark Ke ISP1 dan ISP2
  ```
  ip route add dst-address=0.0.0.0/0 gateway=192.168.111.1 routing-mark=pc1
  ```
    ```
  ip route add dst-address=0.0.0.0/0 gateway=192.168.122.1 routing-mark=pc2
  ```
  <br> Tampilan routing mark di Winbox
  <img width="1193" height="356" alt="Image" src="https://github.com/user-attachments/assets/32b62c51-0481-4ba0-bd4f-dc09100ec54e" />
- **Konsep Main Routing**
  
  <br> Tampilan di CLI
  <img width="874" height="205" alt="Image" src="https://github.com/user-attachments/assets/e0bad57e-816a-4077-b36a-f35c3862e084" />
  <br> Cara rubah gateway di baris ke 2
  ```
  ip route set 2 gateway=192.168.122.1
  ```
- **Load Balance Routing Mark (Firewall Mangle)**
- **Address List untuk Mangle**
