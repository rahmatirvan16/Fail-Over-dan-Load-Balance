- **Konsep Fail Over & Load Balance**
  <br>Fail Over adalah Settingan Mikrotik dengan Setingan 1 Aktif dan 1 Backup
  <br>Load Balance adalah Setingan Mikrotik dengan kedua ISP Aktif (sebgaian ke ISP Pertama dan sebagian ke ISP Kedua)
- **Konfigurasi Fail Over**
- **Check Gateway**
  <br>adalah fitur untuk setting automasi ISP lebih dari 1 ke ISP aktif, jika saat ping menghasilkan time out
  ```
  ip route set 0 check-gateway=ping
  ``` 
- **Load Balance ECMP**
- **Load Balance Routing Mark (Route Rules)**
- **Konsep Main Routing**
- **Load Balance Routing Mark (Firewall Mangle)**
- **Address List untuk Mangle**
