---
title: "Lab 2 - Enable Billing Access"
date: 2025-08-11T10:15:00+07:00
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

#### Mục tiêu
- Kích hoạt quyền **IAM User and Role Access to Billing Information**.
- Cho phép IAM user có thể xem thông tin Billing & Cost trong AWS Console.
- Kết quả: IAM user đăng nhập có thể truy cập mục **Billing**.

---

### Chuẩn bị (trước khi bắt đầu)
- AWS account với quyền AdministratorAccess hoặc quyền quản lý **Account Settings**.
- Đã có IAM user cần bật quyền Billing access.
- Trình duyệt đăng nhập vào **AWS Management Console**.

---

#### Bước 1. Mở trang Account Settings
1. Đăng nhập **AWS Management Console**.  
2. Chọn **Account** trong mục **AWS Account Settings**.

![Error Picture](/static/images/AWS-Pic/accout.png)

![Error Picture](/static/images/AWS-Pic/click-accout.png)
---

#### Bước 2. Truy cập mục IAM User and Role Access to Billing Information
1. Cuộn xuống dưới tới phần **IAM User and Role Access to Billing Information**.
2. Click **Edit** ở góc phải.

![Error Picture](/static/images/AWS-Pic/billing-edit.png)

---

#### Bước 3. Bật quyền IAM Access cho Billing
1. Tick vào **Activate IAM Access**.
2. Nhấn **Update** để lưu thay đổi.

![Error Picture](/static/images/AWS-Pic/billing-activate.png)

---

### Kết quả mong đợi
![Error Picture](/static/images/AWS-Pic/billing-done.png)

- IAM user có thể truy cập mục **Billing** trong AWS Console.
