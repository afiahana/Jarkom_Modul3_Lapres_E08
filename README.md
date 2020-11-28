# Jarkom_Modul3_Lapres_E08

## 1. Membuat topologi jaringan
- Membuat file topologi.sh dengan isian
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.70.37 eth1=daemon,,,switch1 eth2=daemon,,,switch3 eth3=daemon,,,switch2 mem=256M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=160M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
xterm -T TUBAN -e linux ubd0=TUBAN,jarkom umid=TUBAN eth0=daemon,,,switch2 mem=128M &

# Klien
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=64M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=64M &
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch3 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch3 mem=64M &
```

## 2. SURABAYA ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client
- Pada UML Surabaya, membuka file dengan cara ``` nano /etc/sysctl.conf ```
- Uncomment dan mengubah menjadi ``` net.ipv4.conf.all.accept_source_route = 1 ```
- Simpan lalu jalankan ``` sysctl -p ```
- Install DHCP Relay dengan ``` apt-get install isc-dhcp-relay ```
- Buka file ``` nano /etc/default/isc-dhcp-relay ```
- Konfigurasi seperti gambar di bawah ini

- Pada UML Tuban, buka file ``` nano /etc/dhcp/dhcpd.conf ```
- Konfigurasi seperti gambar di bawah ini



## 3. Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200
- Pada UML Tuban, buka file ``` nano /etc/dhcp/dhcpd.conf ```
- Konfigurasi seperti gambar di bawah ini

- Jalankan ``` service dhcp restart ```
- Pada UML Gresik dan Sidoarjo (Subnet 1), buka file ``` nano /etc/network/interfaces ```
- Konfigurasi seperti gambar di bawah ini

- Cek keberhasilan di UML Sidoarjo dan/atau Gresik dengan ``` cat /etc/resolv.conf ```


## 4. Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70
- Pada UML Tuban, buka file ``` nano /etc/dhcp/dhcpd.conf ```
- Konfigurasi seperti gambar di bawah ini

- Jalankan ``` service dhcp restart ```
- Pada UML Banyuwangi dan Madiun (Subnet 1), buka file ``` nano /etc/network/interfaces ```
- Konfigurasi seperti gambar di bawah ini

- Cek keberhasilan di UML Banyuwangi dan/atau Madiun dengan ``` cat /etc/resolv.conf ```

## 5. Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
- Pada UML Tuban, buka file ``` nano /etc/dhcp/dhcpd.conf ```
- Konfigurasi seperti gambar di bawah ini

- Jalankan ``` service dhcp restart ```
- Cek keberhasilan di semua UML Client dengan ``` cat /etc/resolv.conf ```

## 6. Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit
- Pada UML Tuban, buka file ``` nano /etc/dhcp/dhcpd.conf ```
- Konfigurasi seperti gambar di bawah ini

- Jalankan ``` service dhcp restart ```

## 7. Akses ke proxy hanya bisa dilakukan oleh Anri sendiri sebagai user TA

## 8. Anri sudah menjadwal pengerjaan TA-nya (8) setiap hari Selasa-Rabu pukul 13.00-18.00

## 9. Jadwal bimbingan dengan Bu Meguri adalah (9) setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00)

## 10. Agar Anri bisa fokus mengerjakan TA, (10) setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id agar Anri selalu ingat untuk mengerjakan TA🙂

## 11. Bu Meguri meminta Anri untuk mengubah error page default squid

## 12. Karena Bu Meguri dan Anri adalah tipe orang pelupa, maka untuk memudahkan mereka, Anri memiliki ide ketika menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080
