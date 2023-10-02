---
title : "Di chuyển Object"
date :  "`r Sys.Date()`" 
weight : 9
chapter : false
pre : " <b> 9. </b> "
---

#### Di chuyển Object

- Với hành động **move** (di chuyển) trong bảng điều khiển S3, bạn có thể di chuyển một object đến một thư mục khác trong cùng một bucket, hoặc sang bucket khác.

![Static website](/images/8-moveobject/0000.png?featherlight=false&width=50pc)

1. Tiếp theo chúng ta sẽ tạo **bucket** mới

    - Trong giao diện **S3 bucket**, chọn **Create bucket**

    ![Static website](/images/8-moveobject/0001.png?featherlight=false&width=90pc)

    - Tại mục **Bucket name**, nhập ``aws-first-cloud-journey-move``
    - Tại mục **AWS region**, chọn **Asia Pacific (Singapore) ap-southeast-1** là region có khoảng cách địa lý gần với người dùng Việt Nam nhất tại thời điểm tháng 9 năm 2023

    ![Static website](/images/8-moveobject/0002.png?featherlight=false&width=90pc)

    - Giữ nguyên các giá trị mặc định, cuộn xuống cuối trang, chọn ``Create bucket``

    ![Static website](/images/8-moveobject/0003.png?featherlight=false&width=90pc)

2. Di chuyển file giữa các **Bucket**

    - Trong giao diện **Amazon S3**, chọn bucket **aws-first-cloud-journey**

    ![Static website](/images/8-moveobject/0004.png?featherlight=false&width=90pc)

    - Tích vào ký hiệu **ô vuông** kế giá trị **Name** để chọn toàn bộ Object đang có trong bucket

    - Chọn **Action**, chọn **Calculate total size**

    ![Static website](/images/8-moveobject/0005''.png?featherlight=false&width=90pc)

    - **Kết quả**: bạn đang có tổng cộng 182 objects tương ứng với 21.2 MB, chọn **Close** để quay lại

    ![Static website](/images/8-moveobject/0005'.png?featherlight=false&width=90pc)

    - Tích vào ký hiệu **ô vuông** kế giá trị **Name** để chọn toàn bộ Object đang có trong bucket

    - Chọn **Action**, chọn **Move**

    ![Static website](/images/8-moveobject/0005.png?featherlight=false&width=90pc)

    - Cuộn xuống giữa trang, tại mục **Destination type**, chọn **Bucket**, chọn **Browse S3**

    ![Static website](/images/8-moveobject/0006.png?featherlight=false&width=90pc)

    - Chọn **S3 Buckets**

    ![Static website](/images/8-moveobject/0007.png?featherlight=false&width=90pc) 

    - Chọn bucket name **aws-first-cloud-journey-move**, chọn **Choose destination**

    ![Static website](/images/8-moveobject/0008.png?featherlight=false&width=90pc) 

    - Cuộn xuống cuối trang, tại mục **Additional checksums** giữ nguyên mặc định **Copy existing checksum functions**, chọn **Move**

    - **Noted**: Amazon S3 sử dụng **checksum** để xác minh tính toàn vẹn của dữ liệu mà bạn tải lên hoặc tải xuống hoặc sao chép dữ liệu của mình từ S3

    ![Static website](/images/8-moveobject/0009.png?featherlight=false&width=90pc)

    - Chúc mừng bạn đã move file thành công, chọn **Close**

    ![Static website](/images/8-moveobject/00010.png?featherlight=false&width=90pc)

3. Kiểm tra Object trong Bucket mới

    - Trong giao diện **Amazon S3**, chọn bucket name **aws-first-cloud-journey-move**

    ![Static website](/images/8-moveobject/00011.png?featherlight=false&width=90pc)

    - Tích vào ký hiệu **ô vuông** kế giá trị **Name** để chọn toàn bộ Object đang có trong bucket

    - Chọn **Action**, chọn **Calculate total size**

    ![Static website](/images/8-moveobject/00012.png?featherlight=false&width=90pc)

    - **Kết quả**: bạn đang có tổng cộng 182 objects tương ứng với 21.2 MB -> tương đồng với lần tính toán tổng kích thước của bucket **aws-first-cloud-journey**

    ![Static website](/images/8-moveobject/00013.png?featherlight=false&width=90pc)








