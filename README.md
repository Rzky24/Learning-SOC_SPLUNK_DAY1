# Learning-SOC_SPLUNK_DAY1 Brute Force SSH

# Praktik Coba Query Di Splunk  :
index=firewall_logs dest_port=22
| stats count by src_ip
| sort -count

<img width="1351" height="691" alt="Splunk day 1" src="https://github.com/user-attachments/assets/fda54e6e-9fc8-4f16-bc87-6b023bfd614d" />



# Penjelasan :
index=firewall_logs dest_port=22  : Ambil log firewall yang menuju port SSH (22)

| stats count by src_ip, action : Hitung berapa kali IP muncul  Pisahkan berdasarkan ALLOW / DENY

| sort -count : IP paling sering muncul ditaruh di atas Ini cara SOC menemukan penyerang cepat


# ATOMIC DOCUMENTATION
Context : Firewall mendeteksi koneksi berulang ke port SSH

Action  : Query Splunk untuk menghitung akses berdasarkan IP sumber

Result  : IP 185.220.101.45 melakukan koneksi berulang dan terindikasi brute force













berikut contoh File latihan nya 
====================================
SOC SPLUNK DAILY TRAINING - DAY 1
====================================

SKENARIO:
Terdapat laporan SOC bahwa server internal mengalami
banyak percobaan koneksi ke port SSH (22).

------------------------------------
[1] SAMPLE LOG (firewall.log)
------------------------------------
2025-01-20 08:12:01 firewall action=ALLOW protocol=TCP src_ip=185.220.101.45 dest_ip=192.168.1.10 dest_port=22
2025-01-20 08:12:03 firewall action=ALLOW protocol=TCP src_ip=185.220.101.45 dest_ip=192.168.1.10 dest_port=22
2025-01-20 08:12:05 firewall action=ALLOW protocol=TCP src_ip=185.220.101.45 dest_ip=192.168.1.10 dest_port=22
2025-01-20 08:12:07 firewall action=DENY  protocol=TCP src_ip=185.220.101.45 dest_ip=192.168.1.10 dest_port=22
2025-01-20 08:12:09 firewall action=DENY  protocol=TCP src_ip=185.220.101.45 dest_ip=192.168.1.10 dest_port=22

------------------------------------
[2] TUGAS ANALISIS
------------------------------------
1. Log apa ini?
2. Port apa yang menjadi target?
3. IP mana yang mencurigakan?
4. Dugaan serangan apa yang terjadi?

------------------------------------
[3] MICRO PRACTICE - SPLUNK QUERY
------------------------------------
index=firewall_logs dest_port=22
| stats count by src_ip, action
| sort -count

Tujuan:
Menemukan IP yang sering mengakses SSH

------------------------------------
[4] ATOMIC DOCUMENTATION
------------------------------------
Context :
Action  :
Result  :

====================================
END OF DAY 1
====================================
