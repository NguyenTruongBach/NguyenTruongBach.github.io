---
title: "Giới thiệu"
date: 2025-08-11T10:00:00+07:00
weight: 1
chapter: false
pre: " <b> 1. </b> "
---

#### Giới thiệu

Trong bối cảnh các ứng dụng SaaS (Software as a Service) ngày càng phổ biến, mô hình **Multi-Tenant Database Architecture** trở thành giải pháp quan trọng giúp doanh nghiệp tối ưu chi phí, đơn giản hóa quản lý hạ tầng, đồng thời vẫn đảm bảo tính bảo mật và khả năng mở rộng. Trên nền tảng AWS, kiến trúc này cho phép nhiều khách hàng (tenant) cùng chia sẻ một hệ thống cơ sở dữ liệu, nhưng dữ liệu của mỗi khách hàng vẫn được phân tách và bảo vệ an toàn.

Đề tài "Triển khai Multi-Tenant Database Architecture trên AWS" sẽ hướng dẫn bạn từng bước thiết kế, triển khai và vận hành một hệ thống SaaS cơ bản sử dụng mô hình **Shared Database – Shared Schema**, kết hợp với các dịch vụ AWS như RDS, Elastic Beanstalk, Cognito và CloudWatch. Qua workshop này, bạn sẽ hiểu rõ nguyên lý hoạt động của kiến trúc đa tenant, nắm được cách triển khai thực tế, và có thể áp dụng vào các dự án SaaS.

#### Kiến trúc giải pháp và các dịch vụ sử dụng

Giải pháp Multi-Tenant Database Architecture trên AWS được xây dựng dựa trên các dịch vụ AWS sau:

- **Amazon RDS (PostgreSQL/MySQL)**: Lưu trữ cơ sở dữ liệu đa tenant.
- **AWS Elastic Beanstalk**: Triển khai và quản lý backend API.
- **Amazon Cognito**: Xác thực và phân quyền người dùng, lưu thông tin `tenant_id`.
- **Amazon S3**: Lưu trữ nội dung tĩnh (frontend, tài liệu).
- **Amazon CloudWatch**: Giám sát hiệu suất và log hệ thống.
- **AWS Lambda** *(tùy chọn)*: Xử lý tác vụ nền hoặc automation.
- **Amazon SNS** *(tùy chọn)*: Gửi thông báo khi có sự kiện hệ thống.

Các dịch vụ này phối hợp để tạo ra một giải pháp SaaS đơn giản nhưng hiệu quả, giúp tối ưu chi phí, tăng khả năng mở rộng và đảm bảo an toàn dữ liệu cho từng tenant.
