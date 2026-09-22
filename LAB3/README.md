# LAB 3 – NHẬN DIỆN VÀ ỨNG PHÓ CÁC MỐI ĐE DỌA ĐẾN AN TOÀN THÔNG TIN

## 1. Thông tin sinh viên

* **Họ và tên:** [Đinh Ngọc Kim Ngân]
* **MSSV:** [1150080067]
* **Mã lớp:** [11thmt]
* * **Tên học phần:** An toàn Hệ thống Thông tin
* **Tên bài lab:** Lab 3 – Nhận diện và ứng phó các mối đe dọa đến an toàn thông tin

---

## 2. Môi trường thực hành

### Máy ảo

* **Nền tảng ảo hóa:** VMware Workstation Pro 26H1
* **Hệ điều hành:** Windows 11 25H2 x64
* **OS Build:** 26200.9445
* **Network Adapter:** Host-only
* **Snapshot sạch:** LAB3_CLEAN_20260914

### Công cụ

* **Microsoft Defender Antivirus:** Tích hợp Windows 11
* **Sysmon:** 15.22
* **Autoruns:** 14.3
* **Process Explorer:** 17.14
* **Wireshark:** 4.6.8
* **Python:** 3.14.7
* **Npcap:** sử dụng để capture loopback traffic trên Windows

---

## 3. Cách dựng môi trường

### Bước 1 – Tạo máy ảo

Tạo máy ảo Windows 11 25H2 trên VMware Workstation Pro 26H1.

Cấu hình mạng:

```text
Network Adapter = Host-only
```

Sau khi cập nhật hệ điều hành, tạo snapshot:

```text
LAB3_CLEAN_20260914
```

### Bước 2 – Tạo thư mục LAB3

```text
C:\LAB3
├── Evidence
├── Tools
├── Downloads
└── Assets
```

### Bước 3 – Chuẩn bị bộ dữ liệu

Sao chép:

```text
LAB3_Threats_Assets.zip
```

vào:

```text
C:\LAB3\Downloads
```

Kiểm tra SHA-256 trước khi giải nén và giải nén bộ dữ liệu vào `C:\LAB3`.

### Bước 4 – Cài đặt công cụ

Cài đặt và kiểm tra:

```text
Python 3.14.7
Wireshark 4.6.8
Sysmon 15.22
Autoruns 14.3
Process Explorer 17.14
```

Các executable của Sysinternals được tải từ nguồn Microsoft Sysinternals theo hướng dẫn của bài lab.

---

## 4. Các tình huống đã thực hiện

### TH1 – Asset, Vulnerability, Threat, Risk và Control

* Xây dựng Risk Register.
* Xác định tài sản, lỗ hổng, mối đe dọa, rủi ro và biện pháp kiểm soát.
* Phân loại 5 nguồn đe dọa:

  * Hành động vô ý
  * Hành động cố ý
  * Thảm họa tự nhiên
  * Lỗi kỹ thuật
  * Lỗi quản lý

**Kết quả:** PASS

### TH2 – Malware / EICAR

* Kiểm tra Microsoft Defender và Real-time Protection.
* Tạo EICAR test file trong phạm vi bài lab.
* Kiểm tra detection bằng PowerShell.
* Đối chiếu với Windows Security – Protection History.
* Không tắt Defender và không tạo exclusion.

**Kết quả:** PASS

### TH3 – Password và nguy cơ Keylogging

* Bật Audit Logon success/failure.
* Tạo tài khoản thử nghiệm `lab3user`.
* Tạo đăng nhập thành công và đăng nhập thất bại có kiểm soát.
* Phân tích Event ID 4624, 4625 và 4648.
* Đổi mật khẩu và kiểm tra credential cũ/mới.

**Kết quả:** PASS

### TH4 – Persistence và Listener

* Cài đặt Sysmon.
* Kiểm tra Event ID 1 – Process Create.
* Tạo Run Value `LAB3_Run_Demo`.
* Tạo Scheduled Task `LAB3_Persistence_Demo`.
* Kiểm tra persistence bằng Autoruns.
* Chạy HTTP server chỉ trên `127.0.0.1:8080`.
* Ánh xạ port với PID bằng PowerShell.
* Kiểm tra process bằng Process Explorer.

**Kết quả:** PASS

### TH5 – Sniffing / MITM / Spoofing

* Capture HTTP loopback traffic bằng Wireshark.
* Kiểm tra dữ liệu HTTP plaintext trong Request URI.
* Capture TLS/HTTPS traffic.
* So sánh dữ liệu quan sát được giữa HTTP và HTTPS.
* Không thực hiện ARP poisoning, DNS spoofing hoặc MITM chủ động.

**Kết quả:** PASS

### TH6 – DoS / DDoS / Mail Bombing

* Thực hiện local load test trên `127.0.0.1:8080`.
* Phân tích `ddos_sample.csv`.
* Phân tích `mailbomb_sample.csv`.
* Không tạo DDoS thực tế và không gửi email hàng loạt.

**Kết quả:** PASS

### TH7 – Social Engineering / Phishing / Spear Phishing

* Phân tích mẫu `phishing_email.txt` offline.
* Nhận diện các dấu hiệu phishing.
* Phân loại 6 tình huống trong `social_engineering_cases.csv`.
* Xác định biện pháp phòng tránh phù hợp.

**Kết quả:** PASS

---

## 5. Cleanup và Recovery

Sau khi thu thập đầy đủ bằng chứng:

* Xóa `LAB3_Run_Demo`.
* Xóa `LAB3_Persistence_Demo`.
* Dừng HTTP server trên port 8080.
* Xóa tài khoản thử nghiệm `lab3user`.
* Kiểm tra lại persistence và listener.
* Kiểm tra Microsoft Defender vẫn hoạt động.
* So sánh `autoruns_before.csv` và `autoruns_after.csv`.
* Tạo `evidence_sha256.csv`.
* Khôi phục máy ảo về snapshot sạch.

**Kết quả:** PASS

---

## 6. Bằng chứng

Các bằng chứng của bài được lưu trong thư mục `Evidence`.

Một số bằng chứng chính:

```text
H1_VM_WindowsVersion.png
H2_ToolVersions.png
H3_Baseline_Defender_Firewall.png
H4_ProtectionHistory_EICAR.png
H5_Event4625.png
H6_Sysmon_Event1.png
H7_Autoruns_LAB3_Run_Demo.png
H8_ProcessExplorer_Python.png
H9_HTTP_Plaintext.png
H10_TLS_443.png
H10_Load_and_Log_Analysis.png
H10_Phishing_Offline.png
H11_Recovery_Verification.png
```

Các file log/output gồm:

```text
baseline_os.txt
baseline_defender.txt
baseline_firewall.txt
baseline_network.txt
baseline_processes.txt
defender_eicar.txt
auth_events_before_rotation.txt
autoruns_before.csv
autoruns_after.csv
autoruns_diff.txt
sysmon_persistence.txt
local_load_test.txt
ddos_sources.txt
mail_sender_counts.txt
mail_volume.txt
evidence_sha256.csv
```

---

## 7. Kết quả tổng hợp

| Tình huống | Nội dung                                   | Kết quả |
| ---------- | ------------------------------------------ | ------- |
| TH1        | Risk Register và phân loại nguồn đe dọa    | PASS    |
| TH2        | EICAR và Defender Detection                | PASS    |
| TH3        | Authentication Events và Password Rotation | PASS    |
| TH4        | Sysmon, Persistence và Local Listener      | PASS    |
| TH5        | HTTP/HTTPS Capture bằng Wireshark          | PASS    |
| TH6        | Local Load, DDoS Dataset và Mail Log       | PASS    |
| TH7        | Phishing và Social Engineering             | PASS    |
| Recovery   | Cleanup, Hash và Snapshot Recovery         | PASS    |

---

## 8. Lỗi gặp phải và cách khắc phục

### Lỗi 1

**Mô tả:** [Ghi lỗi thực tế nếu có]

**Nguyên nhân:** [Nguyên nhân]

**Cách khắc phục:** [Cách đã xử lý]

### Lỗi 2

**Mô tả:** [Ghi lỗi thực tế nếu có]

**Nguyên nhân:** [Nguyên nhân]

**Cách khắc phục:** [Cách đã xử lý]

Nếu không gặp lỗi:

```text
Không phát sinh lỗi nghiêm trọng trong quá trình thực hành.
```

---

## 9. Phạm vi an toàn

Bài thực hành được thực hiện trong máy ảo và trong phạm vi được quy định.

* Traffic gây tải chỉ sử dụng `127.0.0.1:8080`.
* Không thực hiện DDoS thực tế.
* Không gửi mail bombing.
* Không thực hiện MITM chủ động.
* Không sử dụng tài khoản, mật khẩu, token, cookie hoặc dữ liệu cá nhân thật.
* Không tắt Microsoft Defender/Tamper Protection.
* Không đưa installer, executable hoặc file bị Defender quarantine lên GitHub.

---

## 10. Video thực hành

**Link video:** [Dán link video tại đây nếu lớp yêu cầu]

---

## 11. Repository

Repository bài LAB3:

[ Dán link GitHub repository tại đây ]
