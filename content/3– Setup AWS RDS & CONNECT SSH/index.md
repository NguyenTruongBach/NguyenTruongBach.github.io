---
title: "Lab 3 – Tạo RDS và EC2 kết nối qua SSH"
date: 2025-08-11T14:20:00+07:00
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

#### Mục tiêu

- Tạo cơ sở dữ liệu **Amazon RDS** (PostgreSQL hoặc MySQL).
- Tạo máy chủ **EC2** để kết nối tới RDS.
- Kết nối vào EC2 qua SSH.
- Kết quả: EC2 có thể kết nối đến RDS.

---

### Chuẩn bị (trước khi bắt đầu)

- AWS account với quyền quản trị.
- Đã đăng nhập vào **AWS Management Console**.
- Trình duyệt và kết nối internet ổn định.

---

## Bước 1 – Tạo RDS Instance

1. Truy cập **AWS Management Console** → tìm và mở dịch vụ **RDS**.

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/RDS.png)

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/RDS_DTB.png)

2. Chọn **Create database**.

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/CREATE_DB.png)

3. Chọn:
   - **Creation method**: Standard create
   - **Engine type**: PostgreSQL (hoặc MySQL nếu yêu cầu)

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/Clickchoice.png)

- **Version**: Chọn bản mới nhất.

4. **Templates**: chọn **Free tier**

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/Template.png)

5. **Settings**:
   - DB instance identifier: `lab3-ws`
   - Master username: `postgres` (hoặc tên tùy chọn)
   - Master password: nhập và xác nhận.
6. **Instance configuration**:
   - Chọn loại máy: `db.t3.micro` (Free tier) hoặc cấu hình phù hợp.
7. **Storage**:

   - Allocated storage: 20 GiB
   - Tắt `Enable storage autoscaling` để tạo nhanh.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/enable.png)

8. **Connectivity**:

   - VPC: chọn VPC mặc định hoặc VPC lab yêu cầu.
   - Public access: **Yes**.

     ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/pulic_access.png)

9. Các mục **Monitoring**, **Backup**, **Maintenance** để mặc định hoặc tắt nếu lab yêu cầu.
10. Nhấn **Create database** và chờ RDS trạng thái **Available**.

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_create.png)

## ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_RDS.png)

## Bước 2 – Tạo EC2 Instance

1. Truy cập **AWS Management Console** → mở dịch vụ **EC2** → **Launch instance**.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/EC2.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/instances.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/launch_instances.png)

2. **Name and tags**: `lab3-ec2`.
3. **Application and OS Images**:
   - Chọn Amazon Linux 2023 (Amazon Linux AMI) – tối ưu cho SSH demo.
4. **Instance type**: `t2.micro` (Free tier).
5. **Key pair**:
   - Chọn **Create new key pair**:
     - Name: `lab3-key`
     - Type: RSA
     - Format: `.pem`
     - Nhấn **Create key pair** → file `.pem` được tải xuống.
6. **Network settings**:

   - VPC: Chọn cùng VPC với RDS.
   - Subnet: cùng AZ hoặc mặc định.
   - Auto-assign public IP: **Enable**.
   - Security group: **Create new** và add rule:

     - Type: SSH (port 22)
     - Source: My IP.

     ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/network_setting.png)

7. Nhấn **Launch instance** và chờ trạng thái **Running**.
   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_launch.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_screen.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/running.png)

---

## Bước 3 – Kết nối SSH vào EC2

1. Mở terminal (hoặc Git Bash) trên máy.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/gitbash.png)

   Gõ lệnh "cd ~/Downloads
   mv "lab3 key.pem" lab3-key.pem
   chmod 400 lab3-key.pem
   ssh -i "lab3-key.pem" ec2-user@<Public-IP-EC2>
   <Public-IP-EC2> lấy từ AWS Console → mục Public IPv4 address của EC2."

2. Khi hoàn thành thì màn hình sẽ hiện lên như thế này.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_ssh.png)
