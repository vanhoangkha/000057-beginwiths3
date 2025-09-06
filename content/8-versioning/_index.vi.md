---
title: "Bucket Versioning"
date: "2025-09-06"
weight: 8
chapter: false
pre: "<b> 8. </b>"
---

#### Giới thiệu

{{% notice info %}}
**Lưu Ý Chi Phí:** Mỗi phiên bản của object được lưu trữ như một bản sao hoàn chỉnh, không chỉ là sự khác biệt. Nếu bạn có 3 phiên bản của một file, bạn sẽ trả tiền cho 3 file hoàn chỉnh. AWS tính phí theo mức giá S3 thông thường cho mỗi phiên bản được lưu trữ và truyền tải. Hãy cân nhắc sử dụng lifecycle policies để quản lý các phiên bản cũ.
{{% /notice %}}

#### S3 Versioning là gì?

**Versioning** trong Amazon S3 là một tính năng cho phép bạn giữ nhiều biến thể của một đối tượng trong cùng một bucket. Khi versioning được bật, bạn có thể bảo toàn, truy xuất và khôi phục mọi phiên bản của mọi đối tượng được lưu trữ trong bucket của mình, cung cấp một lớp bảo vệ dữ liệu bổ sung chống lại việc xóa hoặc sửa đổi ngoài ý muốn.

#### Lợi Ích Chính của Versioning

- **Bảo Vệ Dữ Liệu:** Bảo vệ chống lại việc ghi đè và xóa ngoài ý muốn
- **Theo Dõi Thay Đổi:** Duy trì lịch sử hoàn chỉnh của các sửa đổi đối tượng
- **Khôi Phục Dễ Dàng:** Nhanh chóng khôi phục các phiên bản trước khi cần
- **Tuân Thủ:** Đáp ứng các yêu cầu quy định về lưu giữ dữ liệu
- **Cộng Tác:** Nhiều người dùng có thể làm việc trên cùng các đối tượng một cách an toàn

#### Cách Versioning Hoạt Động

Khi versioning được bật trên một bucket:
- Mỗi đối tượng nhận được một ID phiên bản duy nhất
- Các lần tải lên mới tạo ra các phiên bản mới thay vì ghi đè các đối tượng hiện có
- Các phiên bản trước vẫn có thể truy cập và có thể được truy xuất bất cứ lúc nào
- Các thao tác xóa tạo ra "delete marker" thay vì xóa vĩnh viễn đối tượng

#### Trạng Thái Versioning

Các bucket S3 có thể ở một trong ba trạng thái versioning:
- **Unversioned (mặc định):** Không có versioning, các đối tượng có thể bị ghi đè
- **Versioning-enabled:** Các phiên bản mới được tạo cho mỗi lần tải lên
- **Versioning-suspended:** Không tạo phiên bản mới, nhưng các phiên bản hiện có vẫn còn

#### Thực Hành Tốt Nhất

- **Sử Dụng Lifecycle Policies:** Tự động xóa các phiên bản cũ sau một thời gian xác định
- **Giám Sát Chi Phí:** Versioning có thể tăng đáng kể chi phí lưu trữ
- **MFA Delete:** Bật MFA Delete để bảo mật bổ sung khi xóa phiên bản
- **Cross-Region Replication:** Sao chép các phiên bản qua các vùng để khôi phục thảm họa

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
