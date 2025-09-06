---
title: "Ghi Chú & Thực Hành Tốt Nhất"
date: "2025-09-06"
weight: 12
chapter: false
pre: " <b> 12. </b> "
---

#### Hướng Dẫn Thực Hành Tốt Nhất & Khắc Phục Sự Cố AWS S3

#### Thực Hành Tốt Nhất về Bảo Mật

#### 1. Block Public Access
- **Luôn giữ Block Public Access được bật** trong production
- Sử dụng CloudFront với Origin Access Control (OAC) thay vì public buckets
- Không bao giờ tắt tất cả 4 cài đặt Block Public Access trừ khi thực sự cần thiết

#### 2. Bucket Policies
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipal",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::account-id:distribution/distribution-id"
        }
      }
    }
  ]
}
```

#### 3. Mã Hóa
- Bật mã hóa mặc định (SSE-S3 hoặc SSE-KMS)
- Sử dụng SSE-KMS cho dữ liệu nhạy cảm với chính sách khóa phù hợp
- Cân nhắc mã hóa phía máy khách cho dữ liệu cực kỳ nhạy cảm

#### Thực Hành Tốt Nhất về Hiệu Suất

#### 1. Cấu Hình CloudFront
- Sử dụng Origin Access Control (OAC) thay vì Origin Access Identity (OAI)
- Cấu hình hành vi bộ nhớ đệm và giá trị TTL phù hợp
- Bật nén cho nội dung dạng văn bản
- Sử dụng hỗ trợ HTTP/2 và IPv6

#### 2. S3 Transfer Acceleration
- Bật cho tải lên/tải xuống toàn cầu
- Sử dụng tải lên nhiều phần cho tệp > 100MB
- Triển khai logic thử lại với exponential backoff

#### 3. Mẫu Yêu Cầu
- Tránh tên khóa tuần tự (sử dụng tiền tố ngẫu nhiên)
- Phân phối yêu cầu qua nhiều tiền tố
- Sử dụng S3 Transfer Acceleration cho truy cập toàn cầu

#### Tối Ưu Hóa Chi Phí

#### 1. Lớp Lưu Trữ
- Sử dụng S3 Intelligent-Tiering cho mẫu truy cập không rõ
- Triển khai chính sách vòng đời để chuyển sang lớp lưu trữ rẻ hơn
- Sử dụng S3 Storage Lens để phân tích chi phí

#### 2. Quản Lý Versioning
```json
{
  "Rules": [
    {
      "ID": "DeleteOldVersions",
      "Status": "Enabled",
      "NoncurrentVersionExpiration": {
        "NoncurrentDays": 30
      }
    }
  ]
}
```

#### 3. Truyền Dữ Liệu
- Sử dụng CloudFront để giảm chi phí truyền dữ liệu
- Cân nhắc giá S3 Transfer Acceleration so với truyền tiêu chuẩn
- Giám sát các chỉ số CloudWatch để tối ưu hóa

#### Các Lỗi Thường Gặp & Khắc Phục Sự Cố

#### 1. Lỗi 403 Forbidden
**Triệu chứng:** Không thể truy cập đối tượng S3 qua CloudFront
**Nguyên nhân:**
- Block Public Access được bật nhưng không có thiết lập OAC đúng
- Chính sách bucket không chính xác
- Thiếu quyền CloudFront

**Giải pháp:**
```bash
# Kiểm tra chính sách bucket
aws s3api get-bucket-policy --bucket your-bucket-name

# Xác minh cấu hình CloudFront OAC
aws cloudfront get-origin-access-control --id your-oac-id

# Cập nhật bucket policy cho OAC
aws s3api put-bucket-policy --bucket your-bucket-name --policy file://policy.json
```

#### 2. Website Endpoint vs Bucket Endpoint
**Vấn đề:** Nhầm lẫn giữa S3 website endpoint và bucket endpoint

**S3 Website Endpoint:**
- Format: `bucket-name.s3-website-region.amazonaws.com`
- Hỗ trợ index/error documents
- Không thể sử dụng OAC/OAI
- Phải sử dụng như CloudFront custom origin

**S3 Bucket Endpoint:**
- Format: `bucket-name.s3.region.amazonaws.com`
- Hỗ trợ OAC/OAI
- Bảo mật tốt hơn
- Được khuyến nghị cho CloudFront

#### 3. Lỗi CORS
**Triệu chứng:** Browser chặn requests từ web applications
**Giải pháp:**
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "HEAD"],
    "AllowedOrigins": ["https://yourdomain.com"],
    "ExposeHeaders": ["ETag"],
    "MaxAgeSeconds": 3000
  }
]
```

#### 4. Chi Phí Versioning
**Vấn đề:** Chi phí storage cao bất ngờ
**Monitoring:**
```bash
# Liệt kê object versions
aws s3api list-object-versions --bucket your-bucket-name

# Kiểm tra storage metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/S3 \
  --metric-name BucketSizeBytes \
  --dimensions Name=BucketName,Value=your-bucket-name \
  --start-time 2024-01-01T00:00:00Z \
  --end-time 2024-01-31T23:59:59Z \
  --period 86400 \
  --statistics Average
```

#### Tài Liệu Khuyến Nghị

#### Tài Liệu AWS Chính Thức
- [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/)
- [CloudFront Developer Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/)
- [S3 Security Best Practices](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)

#### AWS Blogs & Whitepapers
- [Amazon S3 Security Best Practices](https://aws.amazon.com/blogs/aws/amazon-s3-security-best-practices/)
- [Optimizing Amazon S3 Performance](https://aws.amazon.com/blogs/aws/amazon-s3-performance-tips-tricks/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

#### Tools & Services
- **AWS Config:** Monitor S3 bucket compliance
- **AWS CloudTrail:** Audit S3 API calls
- **S3 Storage Lens:** Phân tích storage usage và costs
- **AWS Trusted Advisor:** Nhận optimization recommendations

#### Các Lệnh CLI Hữu Ích

#### Quản Lý Bucket
```bash
# Tạo bucket với encryption
aws s3api create-bucket --bucket my-secure-bucket \
  --region us-east-1 \
  --create-bucket-configuration LocationConstraint=us-east-1

# Bật versioning
aws s3api put-bucket-versioning --bucket my-bucket \
  --versioning-configuration Status=Enabled

# Set lifecycle policy
aws s3api put-bucket-lifecycle-configuration --bucket my-bucket \
  --lifecycle-configuration file://lifecycle.json
```

#### Monitoring & Debugging
```bash
# Kiểm tra bucket policy
aws s3api get-bucket-policy --bucket my-bucket

# Liệt kê tất cả versions của objects
aws s3api list-object-versions --bucket my-bucket

# Lấy bucket metrics
aws s3api get-bucket-metrics-configuration --bucket my-bucket \
  --id my-metrics-config
```

#### Danh Sách Kiểm Tra Production

Trước khi deploy lên production:

- [ ] Block Public Access được bật
- [ ] CloudFront sử dụng OAC (không phải OAI)
- [ ] Bucket policy tuân theo nguyên tắc least privilege
- [ ] Default encryption được bật
- [ ] Lifecycle policies được cấu hình
- [ ] Monitoring và alerting được thiết lập
- [ ] Backup và disaster recovery plan tồn tại
- [ ] Cost monitoring được cấu hình
- [ ] Security scanning được implement
- [ ] Access logging được bật

#### Di Chuyển từ Thiết Lập Cũ

Nếu bạn đang sử dụng setup từ tutorial này trong production:

1. **Tạo CloudFront distribution mới với OAC**
2. **Cập nhật DNS để point đến distribution mới**
3. **Test kỹ lưỡng trước khi remove setup cũ**
4. **Bật Block Public Access**
5. **Cập nhật monitoring và alerting**

Lưu ý: Tutorial này dành cho mục đích học tập. Môi trường production cần thêm các cân nhắc về bảo mật và hiệu suất.
