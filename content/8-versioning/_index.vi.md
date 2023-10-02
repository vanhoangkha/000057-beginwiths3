---
title: "Bucket Versioning"
date: "`r Sys.Date()`"
weight: 8
chapter: false
pre: " <b> 8. </b> "
---

#### Giới thiệu

- Tính năng **Versioning** trong **Amazon S3** là một phương thức để giữ nhiều phiên bản của một **object** trong cùng một **bucket**.

- Bạn có thể sử dụng tính năng **versioning** của S3 để bảo toàn, truy xuất và khôi phục mọi phiên bản của mọi **object** được lưu trữ trong **bucket** của bạn.

- Với tính năng **versioning**, bạn có thể khôi phục dễ dàng hơn sau những hành động ngoài ý muốn của người dùng hoặc lỗi ứng dụng. **Versioning** hỗ trợ tạo lập các phiên bản, giúp bạn khôi phục các **object** khỏi việc vô tình xóa bỏ hoặc ghi đè.

- Sau khi tính năng **versioning** được enable cho **bucket** của bạn, nếu **Amazon S3** nhận được nhiều **request** **write** cùng lúc cho cùng một **object** thì nó sẽ lưu trữ tất cả các **object** đó.

![Static website](/images/8'-versioning/0000.png?featherlight=false&width=20pc)

1. Bật tính năng **versioning** của **bucket**

   - Trong giao diện **S3 bucket**, chọn bucket name `aws-first-cloud-journey`

   - Chọn mục **Properties**, tại mục Bucket Versioning, chọn **Edit**

   ![Static website](/images/8'-versioning/0001.png?featherlight=false&width=90pc)

   - Tại mục **Bucket Versioning**, chọn **Enable**, chọn **Save changes**

   ![Static website](/images/8'-versioning/0002.png?featherlight=false&width=90pc)

2. Thay đổi nội dung trên file **index.html**

   - Bật cửa sổ chứa các **folder**, **file** đã down về và giải nén ở [lab 2.2](https://000057.awsstudygroup.com/vi/2-prerequiste/2.2-uploaddata/)

   - Chọn file **index.html** -> nhấn chuột phải -> chọn **Open with** -> chọn **Notepad**

   ![Static website](/images/8'-versioning/0003.png?featherlight=false&width=90pc)

   - Cuộn xuống giữa trang, tại tag **body**, thay giá trị **AWS First Cloud Journey** bằng một nội dung khác, VD: `HỌC CLOUD ^^ VUI BIẾT BAO <3`

   - Trước khi edit:

   ![Static website](/images/8'-versioning/0004.png?featherlight=false&width=90pc)

   - Sau khi edit:

   ![Static website](/images/8'-versioning/0005.png?featherlight=false&width=90pc)

   - Bấm tổ hợp phím: **Ctrl với S** để lưu nội dung vừa edit trên file index.html

3. Test tính năng **versioning** trên **S3**

   - Tại giao diện S3 bucket **AWS First Cloud Journey**, chọn **Upload**

   - Upload file **index.html** vừa edit vào bucket **AWS First Cloud Journey** bằng cách kéo - thả

   ![Static website](/images/8'-versioning/0006.png?featherlight=false&width=90pc)

   - Tại giao diện **Upload**, file index.html trong mục **Files and folders**, cuộn xuống cuối trang và chọn **Upload**

   ![Static website](/images/8'-versioning/0007.png?featherlight=false&width=90pc)

   - Việc **upload** file đã hoàn tất, chọn **Close** để quay về giao diện **bucket**

   ![Static website](/images/8'-versioning/0008.png?featherlight=false&width=90pc)

   - Tại khung search, gõ `index.html` và nhấn enter, lúc này bạn sẽ thấy bucket chỉ hiện ra duy nhất một object. Chuyển nút tròn của **Show versions** từ trái sang phải để thấy version của file.

   ![Static website](/images/8'-versioning/0009.png?featherlight=false&width=90pc)

   - Lúc này bạn đã thấy có **2** file index.html, với thời gian modify của object phía trên gần với thời điểm hiện tại hơn object phía dưới

   ![Static website](/images/8'-versioning/00010.png?featherlight=false&width=90pc)

4. Test tính năng **versioning** trên **Cloudfront**

   - Trong bước [7.3 Kiểm tra Amazon CloudFront](https://000057.awsstudygroup.com/vi/7-cloudfront/7.3-ki%E1%BB%83m_tra_cloudfront/), bạn đã tăng tốc website bằng Cloudfront và thực hiện kiểm tra **Distribution domain name** với nội dung: **AWS FIRST CLOUD JOURNEY**

   ![Static website](/images/8'-versioning/00011.png?featherlight=false&width=90pc)

   - Vậy hãy xem **Default root object** với file `index.html` vừa được upload version mới hơn trên S3 thì nội dung có thay đổi tương ứng với bước 2 ở phía trên hay không!

   - Mở bảng điều khiển Amazon CloudFront tại https://console.aws.amazon.com/cloudfront/home

   - Chọn Distributions ID hiện tại

   ![Static website](/images/8'-versioning/00012.png?featherlight=false&width=90pc)

   - Chọn mục **Behaviors**, chọn dấu tích tròn, chọn **Edit**

   ![Static website](/images/8'-versioning/00013.png?featherlight=false&width=90pc)

   - Tại Cache key and origin requests, chọn **Legacy cache settings**
   - Tại mục Object caching, chọn **Customize**
   - Tại mục Maximum TTL, điền giá tị mới: `0`
   - Tại mụch Default TTL, điền giá tị mới: `0`
   - Cuộn xuống cuối trang, chọn **Save changes**
   - -> Điều này sẽ giúp Cloudfront thường xuyên cập nhật các thay đổi từ S3 trong khuôn khổ bài lab này

   ![Static website](/images/8'-versioning/00014.png?featherlight=false&width=90pc)

   - Bạn cần đợi vài phút để trạng thái chuyển từ **Deploying** sang thời gian lần cuối cùng modify

   ![Static website](/images/8'-versioning/00015.png?featherlight=false&width=90pc)

   ![Static website](/images/8'-versioning/00016'.png?featherlight=false&width=90pc)

   - Sau đó, bạn hãy sao chép Domain name vào trình duyệt để xem nội dung đã thay đổi

   ![Static website](/images/8'-versioning/00016.png?featherlight=false&width=90pc)

   - Tuy nhiên, vào lúc này, bạn muốn nhanh chóng **restore** (khôi phục) lại nội dung cũ mà không cần phải edit file index.html dưới máy local - thì chỉ cần xóa version mới nhất của object: index.html trên S3 bucket

   - Trong giao diện S3 bucket **aws-first-cloud-journey**, tại khung search - bạn nhập `index.html` rồi enter, chọn **Show versions**.

   ![Static website](/images/8'-versioning/00017.png?featherlight=false&width=90pc)

   - Tích vào ký hiệu ô vuông ở phía đầu của object index.html phía trên, chọn **Delete**

   ![Static website](/images/8'-versioning/00018.png?featherlight=false&width=90pc)

   - Kiểm tra đúng file cần xóa -> nhập `permanently delete` vào khung -> chọn **Delete objects**

   ![Static website](/images/8'-versioning/00019.png?featherlight=false&width=90pc)

   - Tại trang trình duyệt đang chạy Domain name của CloudFront, nhấn phím F5 để refesh trang, bạn sẽ nhận được giá trị cũ: **AWS FIRST CLOUD JOURNEY**

   ![Static website](/images/8'-versioning/00020.png?featherlight=false&width=90pc)
