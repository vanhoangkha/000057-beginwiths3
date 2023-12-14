---
title: "Sao chép S3 Object sang region khác"
date: "`r Sys.Date()`"
weight: 10
chapter: false
pre: "<b> 10. </b>"
---

#### Amazon S3 Cross-Region Replication (CRR)

- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/) giúp bạn xây dựng phần **infra** (cơ sở hạ tầng) an toàn, hiệu suất cao, linh hoạt và hiệu quả. Dựa trên 6 trụ cột chính - với pillar **Reliability** sẽ là tinh thần cho bài lab này.

- Để đảm bảo tính **Reliability** (độ tin cậy) của hệ thống, trong bài lab này - các object được lưu trữ trong S3 bucket tại Region Singapore (ap-southeast-1) - nên được **replicate** (sao chép) sang một Region khác.

![Static website](/images/10-s3crr/0000.png?featherlight=false&width=50pc)

- Có nhiều tiêu chí để chọn một Region, ví dụ: **Compliance** (pháp chế), **Latency** (độ trễ), **Cost** (chi phí), **Services and features** (dịch vụ và tính năng). 

- Do đó, trong khuôn khổ bài lab này, để lựa chọn một Region phục vụ cho việc **replicate**, chúng ta sẽ dựa trên tiêu chí: **Cost** (chi phí).

- -> Region N. Virginia (us-east-1) với chi phí S3: 23.55 USD cho 1TB mỗi tháng - rẻ hơn 2.05 USD so với Region Singapore (ap-southeast-1) là một lựa chọn phù hợp với tiêu chí **Cost**. Bạn có thể kiểm tra chi phí tại trang [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=71e120e9a6a9ffe41d37144b4e2c92537b88eb58).

![Static website](/images/10-s3crr/0001.png?featherlight=false&width=90pc)

1. Tiếp theo, chúng ta sẽ tạo **bucket** mới.

    - Trong giao diện **S3 bucket**, chọn **Create bucket**.

    ![Static website](/images/10-s3crr/0002'.png?featherlight=false&width=90pc)

    - Ở mục **Bucket name**, nhập `aws-first-cloud-journey-cross`.
    - Ở mục **AWS region**, chọn **US East (N. Virginia) us-east-1**.

    ![Static website](/images/10-s3crr/0002.png?featherlight=false&width=90pc)

    - Giữ nguyên các giá trị mặc định, cuộn xuống cuối trang và chọn `Create bucket`.

    ![Static website](/images/10-s3crr/0003.png?featherlight=false&width=90pc)

2. Sao chép file giữa các **Bucket** ở các Region khác nhau.

    - Trong giao diện **Amazon S3**, chọn bucket **aws-first-cloud-journey**.

    ![Static website](/images/10-s3crr/0004.png?featherlight=false&width=90pc)

    - Chọn **Management**.

    ![Static website](/images/10-s3crr/0005.png?featherlight=false&width=90pc)

    - Cuộn xuống giữa trang, chọn **Create replication rule**.

    ![Static website](/images/10-s3crr/0006.png?featherlight=false&width=90pc)

    - Ở mục Replication rule name, nhập `PrimaryToSecondary`.
    - Ở mục Status, chọn **Enabled**.
    - Ở mục Choose a rule scope, chọn **Apply to all objects in the bucket**.
    - Ở mục Destination, chọn **Choose a bucket in this account**.
        - **Lưu ý**: có thể chọn **Specify a bucket in another account** để sao chép dữ liệu sang bucket thuộc tài khoản AWS khác. Tuy nhiên, trong bài lab này, chúng ta chỉ chọn sao chép dữ liệu sang bucket khác trong cùng tài khoản AWS.
    - Ở mục Bucket name, chọn **Browse S3**.

    ![Static website](/images/10-s3crr/0007.png?featherlight=false&width=90pc)

    - Chọn bucket **aws-first-cloud-journey-cross**.

    ![Static website](/images/10-s3crr/0008.png?featherlight=false&width=90pc)

    - Bật tính năng **versioning** theo yêu cầu của Amazon S3.
    - Chọn **Enable bucket versioning**.

    ![Static website](/images/10-s3crr/0009.png?featherlight=false&width=90pc)

    - Ở mục IAM role, chọn **Create new role** từ danh sách các vai trò IAM hiện có.

    ![Static website](/images/10-s3crr/00010.png?featherlight=false&width=90pc)

    - Giữ nguyên các giá trị mặc định còn lại và chọn **Save**.

    ![Static website](/images/10-s3crr/00011.png?featherlight=false&width=90pc)

    - Chọn **No, do not replicate existing objects**.

    ![Static website](/images/10-s3crr/00012.png?featherlight=false&width=90pc)

3. Kiểm tra S3 bucket **aws-first-cloud-journey-cross**.

    - Trong giao diện S3 bucket **aws-first-cloud-journey-cross** tại region N. Virginia, kiểm tra xem có object nào chưa.

    ![Static website](/images/10-s3crr/00013.png?featherlight=false&width=90pc)

4. Upload file mới lên S3 bucket **aws-first-cloud-journey**.

    - Tại giao diện S3 bucket **aws-first-cloud-journey**, chọn **Upload**.

    - Chọn thư mục **images** và upload một tấm ảnh bất kỳ.

   ![Static website](/images/10-s3crr/00014.png?featherlight=false&width=90pc)

   - Sau khi upload hoàn tất, chọn **Close**.

   ![Static website](/images/10-s3crr/00015.png?featherlight=false&width=90pc)
   
5. Kiểm tra tính năng **Replication**.

    - Trong giao diện S3, chọn bucket **aws-first-cloud-journey-cross** tại region N. Virginia.

    ![Static website](/images/10-s3crr/00017.png?featherlight=false&width=90pc)

    - Kiểm tra Object.

    ![Static website](/images/10-s3crr/00018.png?featherlight=false&width=90pc)

    - Nếu Object chưa xuất hiện, hãy kiên nhẫn đợi vài phút rồi refresh trang.

    ![Static website](/images/10-s3crr/00019.png?featherlight=false&width=90pc)

    - Kết quả:

    ![Static website](/images/10-s3crr/00020.png?featherlight=false&width=90pc)

    - File hình upload lên S3 bucket **aws-first-cloud-journey** ở bước 4 nay đã xuất hiện tại bucket **aws-first-cloud-journey-cross**.

    - => Bạn đã hoàn thành bài lab replication object giữa các S3 bucket tại hai Region khác nhau.
