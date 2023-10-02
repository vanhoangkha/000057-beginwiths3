---
title : "Sao chép S3 Object sang region khác"
date :  "`r Sys.Date()`" 
weight : 10
chapter : false
pre : " <b> 10. </b> "
---

#### Amazon S3 Cross-Region Replication (CRR)

- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) giúp bạn xây dựng phần **infra** (cơ sở hạ tầng) an toàn, hiệu suất cao, linh hoạt và hiệu quả. Dựa trên 6 trụ cột chính - với pillar **Reliability** sẽ là tinh thần cho bài lab này.

- Để đảm bảo tính **Reliability** (độ tinh cậy) của hệ thống, với bài lab này - là phần data thì các object được lưu trữ trong S3 bucket tại Region Singapore (ap-southeast-1) - nên được **replicate** (sao chép) qua một Region khác.

![Static website](/images/10-s3crr/0000.png?featherlight=false&width=50pc)

- Có nhiều tiêu chí để chọn một Region, ví dụ: **Compliance** (pháp chế), **Latency** (độ trễ), **Cost** (chi phí), **Services and features** (dịch vụ và tính năng). 

- Do đó, trong khuôn khổ bài lab này, để lựa chọn một Region - phục vụ cho việc **replicate** - chúng ta sẽ dựa trên tiêu chí: **Cost** (chi phí). 

- -> Nên Region N. Virginia (us-east-1) với chi phí S3: 23.55 USD cho 1TB mỗi tháng - rẻ hơn 2.05 USD so với Region Singapore (ap-southeast-1) là một lựa chọn phù hợp với tiêu chí **Cost**. Bạn có thể double check chi phí tại trang official của [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=71e120e9a6a9ffe41d37144b4e2c92537b88eb58)

![Static website](/images/10-s3crr/0001.png?featherlight=false&width=90pc)


1. Tiếp theo chúng ta sẽ tạo **buecket** mới

    - Trong giao diện **S3 bucket**, chọn **Create bucket**

    ![Static website](/images/10-s3crr/0002'.png?featherlight=false&width=90pc)

    - Tại mục **Bucket name**, nhập ``aws-first-cloud-journey-cross``
    - Tại mục **AWS region**, chọn **US East (N. Virginia) us-east-1**

    ![Static website](/images/10-s3crr/0002.png?featherlight=false&width=90pc)

    - Giữ nguyên các giá trị mặc định, cuộn xuống cuối trang, chọn ``Create bucket``

    ![Static website](/images/10-s3crr/0003.png?featherlight=false&width=90pc)

2. Sao chép file giữa các **Bucket** ở các Region khác nhau

    - Trong giao diện **Amazon S3**, chọn bucket **aws-first-cloud-journey**

    ![Static website](/images/10-s3crr/0004.png?featherlight=false&width=90pc)

    - Chọn **Management**

    ![Static website](/images/10-s3crr/0005.png?featherlight=false&width=90pc)

    - Cuộn xuống giữa trang, chọn **Create replication rule**

    ![Static website](/images/10-s3crr/0006.png?featherlight=false&width=90pc)

    - Tại mục Replication rule name, nhập ``PrimaryToSecondary``
    - Tại mục Status, giữ nguyên mặc **Enabled**
    - Tại mục Choose a rule scope, chọn **Apply to all objects in the bucket**, tức nghĩa việc cấu hình này sẽ được áp dụng cho toàn bộ objects trong bucket
    - Tại mục Destination, chọn **Choose a bucket in this account**
        - **Noted:** như bạn thấy, chúng ta có thể chọn chức năng **Specify a bucket in another account** tức sao chép dữ liệu qua một bucket thuộc AWS acc khác, tuy nhiên trong khuôn khổ bài lab này, chúng ta chỉ chọn giải pháp sao chép dữ liệu qua một bucket khác nhưng vẫn trong AWS acc hiện tại.
    - Tại mục Bucket name, chọn **Browse S3**

    ![Static website](/images/10-s3crr/0007.png?featherlight=false&width=90pc)

    - Tích ký hiệu tròn để chọn Bucket: **aws-first-cloud-journey-cross**, chọn **Choose path**

    ![Static website](/images/10-s3crr/0008.png?featherlight=false&width=90pc)

    - Lúc này, dịch vụ Amazon S3 yêu cầu bạn phải bật tính năng **versioning** để tiếp tục việc cấu hình, bạn có thể xem lại lab **8. BUCKET VERSIONING** để hiểu thêm khái niệm này.

    - Chọn **Enable bucket versioning**

    ![Static website](/images/10-s3crr/0009.png?featherlight=false&width=90pc)

    - Tại mục IAM role, giữ nguyên mặc định **Choose from existing IAM roles**
    - Chọn ký hiệu tam giác -> bảng giá trị xuất hiện -> chọn **Create new role**

    ![Static website](/images/10-s3crr/00010.png?featherlight=false&width=90pc)
    
    - Giữ nguyên các giá trị mặc định còn lại.
    - Cuộn xuống cuối trang tại mục Additional replication options, chọn **Replication Time Control (RTC)**, với ý nghĩa: S3 RTC sẽ sao chép các Object mà bạn tải lên Amazon S3 qua bucket mới, với thời gian trong vài giây và 99,99% các object đó sẽ hiện diện tại bucket mới trong vòng 15 phút.
    - Chọn **Save**

    ![Static website](/images/10-s3crr/00011.png?featherlight=false&width=90pc)

    - Tại mục, Replicate existing objects?, chọn **No, do not replicate existing objects.**, tức nghĩa chỉ bắt đầu sao chép các object mới upload lên Bucket tại region Singapore qua Bucket tại region N.Virginia

    ![Static website](/images/10-s3crr/00012.png?featherlight=false&width=90pc)

3. Kiểm tra S3 bucket **aws-first-cloud-journey-cross**

    - Trong giao diện, S3 bucket **aws-first-cloud-journey-cross** tại region N. Virginia, bạn có thể nhận thấy chưa có bất kỳ một object nào trong bucket này

    ![Static website](/images/10-s3crr/00013.png?featherlight=false&width=90pc)

4. Upload file mới lên S3 bucket **aws-first-cloud-journey**

    - Tại giao diện S3 bucket **aws-first-cloud-journey**, chọn **Upload**

    - Bật cửa sổ chứa các **folder**, **file** đã down về và giải nén ở [bước 2.2](https://000057.awsstudygroup.com/vi/2-prerequiste/2.2-uploaddata/)

    - Chọn thư mục **images** -> chọn một tấm ảnh bất kỳ -> upload vào bucket **aws-first-cloud-journey** bằng cách kéo - thả

   ![Static website](/images/10-s3crr/00014.png?featherlight=false&width=90pc)

   - Tại giao diện **Upload**, trong mục **Files and folders** xuất hiện file blog-3.jpg, cuộn xuống cuối trang và chọn **Upload**

   ![Static website](/images/10-s3crr/00015.png?featherlight=false&width=90pc)

   - Việc **upload** file đã hoàn tất, chọn **Close** để quay về giao diện **bucket**

   ![Static website](/images/10-s3crr/00016.png?featherlight=false&width=90pc)
   
5. Kiểm tra tính năng **Replication**

    - Trong giao diện S3, chọn bucket **aws-first-cloud-journey-cross** tại region N. Virginia

    ![Static website](/images/10-s3crr/00017.png?featherlight=false&width=90pc)

    - Kiểm tra Object
    - **Noted**: nếu Object chưa xuất hiện, bạn hãy kiên nhẫn vài phút và refresh trang nhé
    ![Static website](/images/10-s3crr/00018.png?featherlight=false&width=90pc)

    - -> Đã có một Object xuất hiện

    - Tích chọn ký hiệu ô vuông trước object **blog-3.jpg**, chọn **Open**

    ![Static website](/images/10-s3crr/00019.png?featherlight=false&width=90pc)

    - Kết quả:

    ![Static website](/images/10-s3crr/00020.png?featherlight=false&width=90pc)

    - -> Tương tự với file hình mà bạn đã upload lên S3 bucket **aws-first-cloud-journey** tại bước 4

    - => Chúc mừng bạn đã hoàn thành bài lab replication object giữa các S3 bucket tại 2 Region khác nhau




