---
title: "Di chuyển Object"
date: "`r Sys.Date()`"
weight: 9
chapter: false
pre: "<b> 9. </b>"
---

#### Di chuyển Object

- Với hành động **move** trong bảng điều khiển S3, bạn có thể di chuyển một object đến một thư mục khác trong cùng một bucket hoặc sang bucket khác.

![Static website](/images/8-moveobject/0000.png?featherlight=false&width=50pc)

1. **Tạo bucket mới**

    - Trong giao diện **S3 bucket**, chọn **Create bucket**.
    
    ![Static website](/images/8-moveobject/0001.png?featherlight=false&width=90pc)

    - Tại mục **Bucket name**, nhập `aws-first-cloud-journey-move`.
    - Tại mục **AWS region**, chọn **Asia Pacific (Singapore) ap-southeast-1**.

    ![Static website](/images/8-moveobject/0002.png?featherlight=false&width=90pc)

    - Giữ nguyên các giá trị mặc định và chọn `Create bucket`.

    ![Static website](/images/8-moveobject/0003.png?featherlight=false&width=90pc)

2. **Di chuyển file giữa các Bucket**

    - Trong giao diện **Amazon S3**, chọn bucket **aws-first-cloud-journey**.
    - Tích vào ký hiệu **ô vuông** kế giá trị **Name** để chọn tất cả Object.
    - Chọn **Action**, sau đó chọn **Calculate total size**.

    ![Static website](/images/8-moveobject/0005''.png?featherlight=false&width=90pc)

    - **Kết quả**: 182 objects, 21.2 MB. Chọn **Close**.

    ![Static website](/images/8-moveobject/0005'.png?featherlight=false&width=90pc)

    - Chọn **Action**, sau đó chọn **Move**.

    ![Static website](/images/8-moveobject/0005.png?featherlight=false&width=90pc)

    - Tại mục **Destination type**, chọn **Bucket** và **Browse S3**.

    ![Static website](/images/8-moveobject/0006.png?featherlight=false&width=90pc)

    - Chọn **S3 Buckets**.

    ![Static website](/images/8-moveobject/0007.png?featherlight=false&width=90pc)

    - Chọn bucket **aws-first-cloud-journey-move** và **Choose destination**.

    ![Static website](/images/8-moveobject/0008.png?featherlight=false&width=90pc)

    - Tại mục **Additional checksums**, giữ nguyên **Copy existing checksum functions** và chọn **Move**.

    ![Static website](/images/8-moveobject/0009.png?featherlight=false&width=90pc)

    - Chọn **Close** sau khi hoàn thành.

    ![Static website](/images/8-moveobject/00010.png?featherlight=false&width=90pc)

3. **Kiểm tra Object trong Bucket mới**

    - Trong giao diện **Amazon S3**, chọn bucket **aws-first-cloud-journey-move**.
    - Tích vào ký hiệu **ô vuông** kế giá trị **Name** để chọn tất cả Object.
    - Chọn **Action**, sau đó chọn **Calculate total size**.

    ![Static website](/images/8-moveobject/00012.png?featherlight=false&width=90pc)

    - **Kết quả**: 182 objects, 21.2 MB.

    ![Static website](/images/8-moveobject/00013.png?featherlight=false&width=90pc)
