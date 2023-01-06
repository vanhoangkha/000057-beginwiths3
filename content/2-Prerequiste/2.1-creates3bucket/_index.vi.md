---
title : "Tạo S3 bucket"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Tạo S3 bucket

1. Đầu tiên, chúng ta sẽ tạo một **S3 bucket**

   - Truy cập **AWS Management Console**
   - Tìm **S3**
   - Chọn **S3**

![Create S3 Bucket](/images/2.1-Creates3bucket/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **S3**, chọn **Create bucket**

![Create S3 Bucket](/images/2.1-Creates3bucket/0002.png?featherlight=false&width=90pc)

3. Trong giao diện **Create bucket**

    - **Bucket name**, nhập **```aws-first-cloud-journey```**
    - **AWS Region**, chọn region bạn muốn.
    - Đối với **Object Ownership**, chọn **ACLs disabled (recommended)**

![Create S3 Bucket](/images/2.1-Creates3bucket/0003.png?featherlight=false&width=90pc)

4. Đối **Block Public Access settings for this bucket**, để mặc định.

![Create S3 Bucket](/images/2.1-Creates3bucket/0004.png?featherlight=false&width=90pc)

5. Kiểm tra lại và chọn **Create bucket**

![Create S3 Bucket](/images/2.1-Creates3bucket/0005.png?featherlight=false&width=90pc)

6. Hoàn thành tạo **S3 bucket** lưu trữ source coe website.

![Create S3 Bucket](/images/2.1-Creates3bucket/0006.png?featherlight=false&width=90pc)
