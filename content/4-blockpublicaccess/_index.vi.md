---
title: "Cấu hình Block Public Access"
date: "2025-09-06"
weight: 4
chapter: false
pre: "<b> 4. </b>"
---

{{% notice warning %}}
**Cảnh Báo Bảo Mật AWS:** AWS khuyến nghị mạnh mẽ giữ Block Public Access được bật. Tutorial này tắt nó cho mục đích học tập, nhưng trong môi trường production, bạn nên sử dụng CloudFront với Origin Access Control (OAC) thay vì làm cho S3 bucket có thể truy cập công khai. Xem [Tài liệu AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html) để biết các lựa chọn an toàn.
{{% /notice %}}

#### Cấu hình Block Public Access

Để truy cập vào website được host, chúng ta cần cấu hình lại **Block Public Access** như sau:

1. Trong giao diện **S3 bucket**:
   - Chọn **Permissions**.
   - Lúc này, bạn sẽ thấy **Block all public access** đang ở trạng thái **On**.

   ![Block Public Access](/images/4-Blockpublicaccess/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **Block public access**:
    - Bỏ chọn **Block all public access**.
    - Chọn **Save changes**.

   ![Block Public Access](/images/4-Blockpublicaccess/0002.png?featherlight=false&width=90pc)

3. Xác nhận bằng cách chọn **Confirm** trong hộp thoại **confirm**.

   ![Block Public Access](/images/4-Blockpublicaccess/0003.png?featherlight=false&width=90pc)

4. Hoàn thành cấu hình **Block Public Access**.

   ![Block Public Access](/images/4-Blockpublicaccess/0004.png?featherlight=false&width=90pc)
