---
title: "Giới thiệu"
date: "2025-09-06"
weight: 1
chapter: false
pre: "<b> 1. </b>"
---

#### Tổng quan

Amazon Simple Storage Service (Amazon S3) là một dịch vụ lưu trữ đối tượng cung cấp khả năng mở rộng theo yêu cầu, đảm bảo tính khả dụng cao của dữ liệu, bảo mật và hiệu suất. S3 được thiết kế để đạt độ bền 99.999999999% (11 số 9) và lưu trữ dữ liệu cho hàng triệu ứng dụng trên toàn thế giới.

#### Amazon S3 là gì?

Amazon S3 là một dịch vụ web cung cấp khả năng mở rộng, tính khả dụng dữ liệu, bảo mật và hiệu suất hàng đầu trong ngành. S3 lưu trữ dữ liệu dưới dạng đối tượng trong các bucket, trong đó mỗi đối tượng có thể có kích thước từ 0 byte đến 5 TB. Với dung lượng lưu trữ hầu như không giới hạn, S3 có thể xử lý bất kỳ lượng dữ liệu nào từ bất cứ đâu trên web.

#### Hiểu về S3 Bucket vs Object

Trước khi bắt đầu bài lab, điều quan trọng là phải hiểu sự khác biệt cơ bản giữa S3 Bucket và Object:

**S3 Bucket:**
- **Là gì**: Container cấp cao nhất chứa các object của bạn
- **Đặt tên**: Phải **duy nhất toàn cầu** trên tất cả tài khoản AWS trên thế giới
- **Vị trí**: Tồn tại trong một AWS Region cụ thể
- **Giới hạn**: Tối đa 100 bucket per tài khoản AWS (có thể tăng)
- **Chức năng**: 
  - Tổ chức và nhóm các object
  - Áp dụng chính sách và quyền
  - Cấu hình tính năng (versioning, encryption, logging)
  - Định nghĩa kiểm soát truy cập

**Ví dụ tên bucket**: `my-website-bucket-2024`

**S3 Object:**
- **Là gì**: Các tệp/dữ liệu thực tế được lưu trữ bên trong bucket
- **Đặt tên**: Key name, chỉ cần duy nhất **trong bucket đó**
- **Kích thước**: Từ 0 byte đến 5TB per object
- **Giới hạn**: Không giới hạn object per bucket
- **Chức năng**:
  - Chứa dữ liệu thực tế (HTML, hình ảnh, video, tài liệu)
  - Có metadata riêng
  - Có thể có quyền riêng lẻ (với ACL)

**Ví dụ object key**: `images/logo.png`, `index.html`, `css/style.css`

**Cấu trúc Mối quan hệ:**
```
Bucket: my-website-bucket
├── index.html (Object)
├── about.html (Object)  
├── css/
│   └── style.css (Object)
└── images/
    ├── logo.png (Object)
    └── banner.jpg (Object)
```

**Ví dụ Đơn giản:**
- **Bucket** = Tủ hồ sơ
- **Object** = Tài liệu bên trong tủ

**Cấu trúc URL:**
- **Bucket**: `https://my-bucket.s3.amazonaws.com/`
- **Object**: `https://my-bucket.s3.amazonaws.com/folder/file.jpg`

**Cấp độ Quyền:**
- **Cấp bucket**: Kiểm soát ai có thể truy cập bucket
- **Cấp object**: Kiểm soát ai có thể truy cập object cụ thể

**Tóm tắt**: Bucket là "container", và object là "nội dung" bên trong container đó.

#### Các Tính Năng Chính

**Lớp Lưu Trữ:**
- **S3 Standard:** Cho dữ liệu được truy cập thường xuyên với độ trễ thấp và thông lượng cao
- **S3 Intelligent-Tiering:** Tự động di chuyển dữ liệu giữa các tầng truy cập để tối ưu chi phí
- **S3 Standard-IA:** Cho dữ liệu ít được truy cập nhưng cần truy cập nhanh khi cần
- **S3 Glacier:** Cho lưu trữ dài hạn với thời gian truy xuất từ phút đến giờ
- **S3 Glacier Deep Archive:** Lưu trữ chi phí thấp nhất cho việc lưu giữ dài hạn

**Bảo Mật & Tuân Thủ:**
- Mã hóa trong quá trình truyền và khi lưu trữ (SSE-S3, SSE-KMS, SSE-C)
- Kiểm soát truy cập thông qua chính sách IAM, chính sách bucket và ACL
- AWS CloudTrail để ghi log và giám sát API
- Tuân thủ các tiêu chuẩn SOC, PCI, HIPAA và các tiêu chuẩn khác

**Quản Lý & Phân Tích:**
- **Versioning:** Giữ nhiều phiên bản của đối tượng để bảo vệ dữ liệu
- **Cross-Region Replication:** Tự động sao chép dữ liệu qua các vùng AWS
- **Lifecycle Management:** Tự động chuyển đổi đối tượng giữa các lớp lưu trữ
- **S3 Storage Lens:** Khả năng hiển thị toàn tổ chức về việc sử dụng và chi phí lưu trữ

**Hiệu Suất & Tính Khả Dụng:**
- SLA khả dụng 99.99% cho S3 Standard
- Tốc độ yêu cầu 3,500 PUT/COPY/POST/DELETE và 5,500 GET/HEAD yêu cầu mỗi giây trên mỗi tiền tố
- Transfer Acceleration sử dụng các edge location của CloudFront
- Tải lên nhiều phần cho các đối tượng lớn

#### Các Trường Hợp Sử Dụng Phổ Biến

S3 phục vụ nhiều trường hợp sử dụng khác nhau trong các ngành công nghiệp:

- **Data Lakes & Phân Tích:** Lưu trữ dữ liệu có cấu trúc và không có cấu trúc cho phân tích dữ liệu lớn
- **Sao Lưu & Khôi Phục:** Giải pháp sao lưu đáng tin cậy với sao chép liên vùng
- **Phân Phối Nội Dung:** Lưu trữ website tĩnh và phân phối nội dung
- **Lưu Trữ Dữ Liệu:** Lưu giữ dài hạn với các lớp lưu trữ Glacier
- **Khôi Phục Thảm Họa:** Dự phòng địa lý cho tính liên tục kinh doanh
- **Lưu Trữ Dữ Liệu Ứng Dụng:** Lưu trữ có thể mở rộng cho ứng dụng di động và web
- **Truyền Thông & Giải Trí:** Lưu trữ và phân phối nội dung video, âm thanh và hình ảnh

#### Lợi Ích

- **Khả Năng Mở Rộng:** Dung lượng lưu trữ hầu như không giới hạn, phát triển theo nhu cầu của bạn
- **Độ Bền:** Độ bền 99.999999999% (11 số 9) bảo vệ chống mất dữ liệu
- **Hiệu Quả Chi Phí:** Chỉ trả tiền cho những gì bạn sử dụng với nhiều tầng giá
- **Bảo Mật:** Bảo mật cấp doanh nghiệp với nhiều tùy chọn mã hóa
- **Tích Hợp:** Tích hợp liền mạch với các dịch vụ AWS khác
- **Truy Cập Toàn Cầu:** Truy cập dữ liệu của bạn từ bất cứ đâu trên thế giới

![S3](/images/icon.png?featherlight=false&width=10pc)
