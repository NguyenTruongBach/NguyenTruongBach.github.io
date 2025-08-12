---
title: "Lab 3 – Create RDS and EC2 with SSH Connection"
date: 2025-08-11T14:20:00+07:00
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

#### Objectives

- Create an **Amazon RDS** database (PostgreSQL or MySQL).
- Create an **EC2** instance to connect to RDS.
- Connect to EC2 via SSH.
- Result: EC2 can connect to RDS.

---

### Prerequisites (before starting)

- AWS account with administrative permissions.
- Logged in to **AWS Management Console**.
- Browser and stable internet connection.

---

## Step 1 – Create an RDS Instance

1. Go to **AWS Management Console** → search for and open the **RDS** service.

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/RDS.png)

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/RDS_DTB.png)

2. Click **Create database**.

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/CREATE_DB.png)

3. Select:
   - **Creation method**: Standard create
   - **Engine type**: PostgreSQL (or MySQL if required)

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/Clickchoice.png)

- **Version**: Choose the latest version.

4. **Templates**: Select **Free tier**.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/Template.png)

5. **Settings**:
   - DB instance identifier: `lab3-ws`
   - Master username: `postgres` (or custom name)
   - Master password: enter and confirm.
6. **Instance configuration**:
   - Instance type: `db.t3.micro` (Free tier) or suitable configuration.
7. **Storage**:

   - Allocated storage: 20 GiB
   - Disable `Enable storage autoscaling` for faster creation.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/enable.png)

8. **Connectivity**:

   - VPC: Select default VPC or lab-required VPC.
   - Public access: **Yes**.

     ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/pulic_access.png)

9. Leave **Monitoring**, **Backup**, **Maintenance** as default or disable if lab requires.
10. Click **Create database** and wait until RDS status is **Available**.

![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_create.png)

## ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_RDS.png)

## Step 2 – Create an EC2 Instance

1. Go to **AWS Management Console** → open **EC2** service → **Launch instance**.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/EC2.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/instances.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/launch_instances.png)

2. **Name and tags**: `lab3-ec2`.
3. **Application and OS Images**:
   - Select Amazon Linux 2023 (Amazon Linux AMI) – optimized for SSH demo.
4. **Instance type**: `t2.micro` (Free tier).
5. **Key pair**:
   - Select **Create new key pair**:
     - Name: `lab3-key`
     - Type: RSA
     - Format: `.pem`
     - Click **Create key pair** → `.pem` file will be downloaded.
6. **Network settings**:

   - VPC: Same VPC as RDS.
   - Subnet: Same AZ or default.
   - Auto-assign public IP: **Enable**.
   - Security group: **Create new** and add rule:

     - Type: SSH (port 22)
     - Source: My IP.

     ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/network_setting.png)

7. Click **Launch instance** and wait until status is **Running**.
   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_launch.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/done_screen.png)

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/running.png)

---

## Step 3 – Connect to EC2 via SSH

1. Open terminal (or Git Bash) on your machine.

   ![Error Picture](/NguyenTruongBach.github.io/static/images/AWS-Pic/gitbash.png)

   Run the following commands:

   ```bash
   cd ~/Downloads
   mv "lab3 key.pem" lab3-key.pem
   chmod 400 lab3-key.pem
   ssh -i "lab3-key.pem" ec2-user@<Public-IP-EC2>
   ```
