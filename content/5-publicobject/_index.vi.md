---
title : "Cấu hình public object"
date :  "`r Sys.Date()`" 
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

#### Cấu hình public object

1. Trong giao diện S3 bucket

    - Chọn **Permissions**

![Public Object](/images/5-publicobject/0001.png?featherlight=false&width=90pc)

2. Kéo giao diện xuống

   - Trong phần **Access control list (ACL)**, chọn **bucket owner enforced**

![Public Object](/images/5-publicobject/0002.png?featherlight=false&width=90pc)

3. Trong giao diện **Object Ownership**

   - Chọn **ACLs enabled**
   - Chọn **I acknowledge that ACLs will be restored**
   - Chọn **Bucket owner preferred**
   - Chọn **Save changes**

![Public Object](/images/5-publicobject/0003.png?featherlight=false&width=90pc)

4. Hoàn thành chỉnh sửa **Object Ownership**

![Public Object](/images/5-publicobject/0004.png?featherlight=false&width=90pc)

5. Quay lại giao diện S3 bucket

    - Chọn **Object**
    - Chọn **Folder** đã tải lên.
    - Chọn **Actions**
    - Chọn **Make public using ACL**

![Public Object](/images/5-publicobject/0005.png?featherlight=false&width=90pc)

6. Trong trang **Make public**

   - Chọn **Make public**

![Public Object](/images/5-publicobject/0006.png?featherlight=false&width=90pc)

7. Hoàn thành cấu hình **public object**

![Public Object](/images/5-publicobject/0007.png?featherlight=false&width=90pc)
