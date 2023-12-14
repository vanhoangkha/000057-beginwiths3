---
title: "Cấu hình Amazon CloudFront"
date: "`r Sys.Date()`"
weight: 2
chapter: false
pre: "<b> 7.2 </b>"
---

Sử dụng bảng điều khiển quản lý AWS để tạo **CloudFront distribution** và cấu hình dịch vụ này phục vụ **s3 Bucket** mà chúng ta đã tạo trước đó.

1. Mở bảng điều khiển Amazon CloudFront tại [đây](https://console.aws.amazon.com/cloudfront/home).
2. Từ bảng điều khiển, nhấn vào **Create a CloudFront distribution**.

    ![CF](/images/cf/7.2/0001.png?featherlight=false&width=90pc)

3. Chỉ định các cài đặt sau cho bản distribution:

    - Trong trường **Origin domain**, chọn S3 bucket mà bạn đã tạo.
    - Trong trường **Origin access**, chọn **Legacy access identities**.

      ![CF](/images/cf/7.2/0002.png?featherlight=false&width=90pc)
 
    - Chọn **Create new OAI** -> giữ nguyên giá trị **name** và chọn **Create** với OAI là Origin access identity.

      ![CF](/images/cf/7.2/0003.png?featherlight=false&width=90pc)

    - Trong trường **Bucket policy**, chọn **Yes, update the bucket policy** để AWS tự động cập nhật quyền cho CloudFront truy cập vào s3 bucket.

      ![CF](/images/cf/7.2/0004.png?featherlight=false&width=90pc)

    - Cuộn xuống gần cuối trang:
        - Tại phần **Web Application Firewall (WAF)**, trong khuôn khổ bài lab này, chọn **Do not enable security protections**.
        - Trong phần **Settings**:
            - Chọn **Use North America, Europe, Asia, Middle East, and Africa**.
            - Tại **Default root object - optional**, điền `index.html` là object bạn đã upload trong bước 2.2 (Tải dữ liệu).
        - Giữ nguyên các giá trị mặc định và chọn **Create distribution**.

      ![CF](/images/cf/7.2/0005.png?featherlight=false&width=90pc)
 
    **Lưu ý**: Trong trường hợp khách hàng thật tế của bạn ở mức toàn cầu, bạn nên chọn **Use all edge locations (best performance)** để phân phối tại [450+ Points of Presence (PoP), 400+ Edge Locations](https://aws.amazon.com/about-aws/global-infrastructure/#:~:text=The%20AWS%20Cloud%20in%20North,two%20Regional%20Edge%20Cache%20locations.).

4. Thông tin **CloudFront**:

    - Sau khi hoàn thành mục 3, AWS sẽ tự động chuyển bạn đến trang thông tin CloudFront với trạng thái là **Deploying**.

      ![CF](/images/cf/7.2/0006.png?featherlight=false&width=90pc)

    **Lưu ý**: Vui lòng đợi trạng thái này trong vài phút - tùy thuộc vào số lượng edge location bạn chọn triển khai. Bạn có thể mở một tab mới để quay lại S3 bucket và xem CloudFront đã thêm những giá trị nào vào bucket policy.

    - Trong giao diện S3 bucket, chọn **Permissions**.

      ![CF](/images/cf/7.2/0007.png?featherlight=false&width=90pc)

    - Tại mục **Bucket policy**, bạn có thể review qua các nội dung quan trọng.

      ![CF](/images/cf/7.2/0008.png?featherlight=false&width=90pc)
