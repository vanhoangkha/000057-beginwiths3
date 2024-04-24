---
title: "Bucket Versioning"
date: "`r Sys.Date()`"
weight: 8
chapter: false
pre: "<b> 8. </b>"
---

#### Giới thiệu

Tính năng **Versioning** trong **Amazon S3** cho phép lưu trữ nhiều phiên bản của một **object** trong cùng một **bucket**. Sử dụng tính năng này, bạn có thể bảo toàn, truy xuất, và khôi phục mọi phiên bản của các **object** trong **bucket**. **Versioning** giúp phục hồi dễ dàng sau những hành động ngoài ý muốn hoặc lỗi ứng dụng. Khi **versioning** được kích hoạt, **Amazon S3** sẽ lưu trữ tất cả các phiên bản của **object** khi có nhiều **request write** cùng lúc.

![Static website](/images/8'-versioning/0000.png?featherlight=false&width=20pc)

#### 1. Bật tính năng **versioning** cho **bucket**

- Truy cập giao diện **S3 bucket**, chọn tên bucket `aws-first-cloud-journey`.
- Chọn **Properties**, sau đó tại mục Bucket Versioning, chọn **Edit**.
  
  ![Static website](/images/8'-versioning/0001.png?featherlight=false&width=90pc)

- Tại mục **Bucket Versioning**, chọn **Enable** và **Save changes**.

  ![Static website](/images/8'-versioning/0002.png?featherlight=false&width=90pc)

#### 2. Thay đổi nội dung file **index.html**

- Mở folder chứa các file đã tải về từ [lab 2.2](https://000057.awsstudygroup.com/vi/2-prerequiste/2.2-uploaddata/).
- Chọn file **index.html**, chuột phải và chọn **Open with > Notepad**.

  ![Static website](/images/8'-versioning/0003.png?featherlight=false&width=90pc)

- Thay đổi nội dung `AWS First Cloud Journey` thành `HỌC CLOUD ^^ VUI BIẾT BAO <3` trong tag **body**.
- Lưu thay đổi bằng tổ hợp phím **Ctrl + S**.

  Trước khi chỉnh sửa:

  ![Static website](/images/8'-versioning/0004.png?featherlight=false&width=90pc)

  Sau khi chỉnh sửa:

  ![Static website](/images/8'-versioning/0005.png?featherlight=false&width=90pc)

#### 3. Kiểm tra tính năng **versioning** trên **S3**

- Truy cập giao diện **S3 bucket AWS First Cloud Journey**, chọn **Upload**.
- Kéo thả file **index.html** đã chỉnh sửa vào bucket.

  ![Static website](/images/8'-versioning/0006.png?featherlight=false&width=90pc)

- Hoàn tất quá trình **upload**, sau đó chọn **Close**.

  ![Static website](/images/8'-versioning/0007.png?featherlight=false&width=90pc)

- Tìm kiếm `index.html`, sau đó kích hoạt **Show versions** để xem các phiên bản của file.

  ![Static website](/images/8'-versioning/0009.png?featherlight=false&width=90pc)

- Bạn sẽ thấy hai phiên bản của file **index.html** với thời gian chỉnh sửa khác nhau.

  ![Static website](/images/8'-versioning/00010.png?featherlight=false&width=90pc)

#### 4. Kiểm tra tính năng **versioning** trên **Cloudfront**

- Truy cập [7.3 Kiểm tra Amazon CloudFront](https://000057.awsstudygroup.com/vi/7-cloudfront/7.3-ki%E1%BB%83m_tra_cloudfront/) và xem **Distribution domain name**.

  ![Static website](/images/8'-versioning/00011.png?featherlight=false&width=90pc)

- Xem liệu **Default root object** có thay đổi sau khi upload phiên bản mới của `index.html` hay không.
- Truy cập **Amazon CloudFront** tại [https://console.aws.amazon.com/cloudfront/home](https://console.aws.amazon.com/cloudfront/home), chọn **Distribution ID** hiện tại.

  ![Static website](/images/8'-versioning/00012.png?featherlight=false&width=90pc)

- Chọn **Behaviors**, sau đó chọn **Edit**.

  ![Static website](/images/8'-versioning/00013.png?featherlight=false&width=90pc)

- Tại **Cache key and origin requests**, chọn **Legacy cache settings**. Tại mục **Object caching**, chọn **Customize** và cài đặt **Maximum TTL** và **Default TTL** là `1`. Sau đó chọn **Save changes**.

  ![Static website](/images/8'-versioning/00014.png?featherlight=false&width=90pc)

- Chờ đến khi trạng thái chuyển từ **Deploying** sang thời gian cuối cùng chỉnh sửa.

  ![Static website](/images/8'-versioning/00015.png?featherlight=false&width=90pc)

  ![Static website](/images/8'-versioning/00016'.png?featherlight=false&width=90pc)

- Sao chép **Domain name** vào trình duyệt để xem thay đổi.

  ![Static website](/images/8'-versioning/00016.png?featherlight=false&width=90pc)

- Để khôi phục nhanh chóng nội dung cũ, xóa phiên bản mới nhất của **index.html** trên **S3 bucket**.

  ![Static website](/images/8'-versioning/00017.png?featherlight=false&width=90pc)

- Chọn object cần xóa và chọn **Delete**.

  ![Static website](/images/8'-versioning/00018.png?featherlight=false&width=90pc)

- Kiểm tra và xác nhận xóa bằng cách nhập `permanently delete` và chọn **Delete objects**.

  ![Static website](/images/8'-versioning/00019.png?featherlight=false&width=90pc)

- Refesh trình duyệt chạy **Domain name** của **CloudFront** để xem nội dung cũ được phục hồi.

  ![Static website](/images/8'-versioning/00020.png?featherlight=false&width=90pc)
