---
title : "Tăng tốc Static Website với Cloudfront"
date :  "`r Sys.Date()`" 
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

#### Giới thiệu

Chúc mừng bạn đã host một trang web tĩnh - thành công trên dịch vụ Amazon S3, nhưng cần phải public S3 của bạn! Vậy làm sao để host một Static Website trên Amazon S3 mà không cần public bất kỳ thông tin nào về bucket của bạn?

Bài lab này sẽ hướng dẫn bạn các bước để lưu trữ nội dung web tĩnh trong [Amazon S3 bucket](https://aws.amazon.com/s3/) , được bảo vệ và tăng tốc bởi [Amazon CloudFront](https://aws.amazon.com/cloudfront/) . Các kỹ năng học được sẽ giúp bạn đảm bảo khối lượng công việc của mình phù hợp với [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc).

![example](/images/cf/s3_user.png?width=50pc)

#### Chi phí

- Thường ít hơn $ 1 mỗi tháng (tùy thuộc vào số lượng request)
- [Giá Amazon S3](https://aws.amazon.com/s3/pricing/)
- [Giá Amazon CloudFront](https://aws.amazon.com/cloudfront/pricing/)
- [Giá Amazon](https://aws.amazon.com/pricing/)

#### Tài liệu tham khảo

- [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

#### Các bước thực hiện

1. [Chặn tất cả truy cập công cộng vào S3](7.1-block_all_public_access/)
2. [Cấu hình Amazon CloudFront](7.2-cấu_hình_amazon_cloudfront/)
3. [Kiểm tra CloudFront](7.3-kiểm_tra_cloudfront/)