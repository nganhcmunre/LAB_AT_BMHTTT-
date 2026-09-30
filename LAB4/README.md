# BÁO CÁO THỰC HÀNH LAB 4
**Chủ đề:** Network Surface Survey and Evaluation using Nmap

## I. CẤU HÌNH MÔ TRƯỜNG LAB
- **Máy tấn công (Attacker):** Kali Linux (Card mạng: Host-Only Adapter)
- **Máy mục tiêu (Target):** Metasploitable 2 (Card mạng: Host-Only Adapter)
- **Dải mạng:** 192.168.56.0/24

## II. XÁC ĐỊNH ĐỊA CHỈ IP
- **Metasploitable 2 IP:** (Điền IP máy Metasploitable2 của bạn vào đây)
- **Kali Linux IP:** (Điền IP máy Kali của bạn vào đây)

## III. KẾT QUẢ RÀ SOÁT MẠNG BẰNG NMAP

### 1. Dò tìm máy hoạt động (Host Discovery)
Lệnh thực hiện:
`nmap -sn 192.168.56.0/24`

### 2. Dò quét cổng & dịch vụ (Port & Service Scan)
Lệnh thực hiện:
`nmap -sV <IP_Metasploitable2>`

Các cổng mở phát hiện được:
- 21/tcp: FTP (vsftpd 2.3.4)
- 22/tcp: SSH (OpenSSH 4.7p1)
- 80/tcp: HTTP (Apache httpd 2.2.8)
- 139/445/tcp: Samba SMB

### 3. Nhận dạng Hệ điều hành (OS Detection)
Lệnh thực hiện:
`sudo nmap -O <IP_Metasploitable2>`
- Kết quả: Linux 2.6.X

### 4. Đánh giá bề mặt tấn công (Aggressive Scan)
Lệnh thực hiện:
`sudo nmap -A <IP_Metasploitable2>`

## IV. ĐÁNH GIÁ VÀ KẾT LUẬN
- Máy mục tiêu Metasploitable 2 chứa nhiều dịch vụ mở lỗi thời và có nguy cơ bị tấn công cao.
- Cần thực hiện đóng các cổng không sử dụng và cập nhật phần mềm lên phiên bản mới nhất.
