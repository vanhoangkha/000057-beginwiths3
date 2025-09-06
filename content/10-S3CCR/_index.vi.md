---
title: "Sao chép S3 Object sang region khác"
date: "2025-09-06"
weight: 10
chapter: false
pre: "<b> 10. </b>"
---

#### Amazon S3 Cross-Region Replication (CRR)

#### Cross-Region Replication là gì?

Amazon S3 Cross-Region Replication (CRR) là một tính năng tự động sao chép các đối tượng giữa các bucket trong các vùng AWS khác nhau. Điều này cung cấp dự phòng địa lý và giúp đáp ứng các yêu cầu tuân thủ đồng thời cải thiện tính khả dụng của dữ liệu và khả năng khôi phục thảm họa.

#### Lợi Ích Chính

- **Khôi Phục Thảm Họa:** Bảo vệ chống lại sự cố vùng và thảm họa
- **Tuân Thủ:** Đáp ứng các yêu cầu quy định về phân phối dữ liệu địa lý
- **Giảm Độ Trễ:** Phục vụ nội dung từ các vùng gần người dùng hơn
- **Chủ Quyền Dữ Liệu:** Giữ bản sao dữ liệu tại các vị trí địa lý cụ thể
- **Xuất Sắc Vận Hành:** Duy trì tính liên tục kinh doanh qua các vùng

#### Cách CRR Hoạt Động

Khi CRR được cấu hình:
- Các đối tượng được tự động sao chép đến các bucket đích trong các vùng khác nhau
- Sao chép xảy ra không đồng bộ, thường trong vòng 15 phút
- Metadata đối tượng, ACL và tag được bảo toàn trong quá trình sao chép
- Versioning phải được bật trên cả bucket nguồn và đích
- Vai trò IAM cung cấp các quyền cần thiết cho quá trình sao chép

#### AWS Well-Architected Framework

[AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/) giúp bạn xây dựng cơ sở hạ tầng an toàn, hiệu suất cao, linh hoạt và hiệu quả. Dựa trên 6 trụ cột chính, với trụ cột **Reliability** (Độ tin cậy) là trọng tâm của bài lab này.

Để đảm bảo tính **Reliability** của hệ thống, các đối tượng được lưu trữ trong S3 bucket tại vùng Singapore (ap-southeast-1) nên được **sao chép** sang một vùng khác để dự phòng và khôi phục thảm họa.

![Static website](/images/10-s3crr/0000.png?featherlight=false&width=50pc)

#### Tiêu Chí Lựa Chọn Vùng

Khi chọn vùng đích để sao chép, hãy xem xét các yếu tố sau:

- **Tuân Thủ:** Yêu cầu quy định về vị trí dữ liệu
- **Độ Trễ:** Khoảng cách đến người dùng cuối để tối ưu hiệu suất
- **Chi Phí:** Chi phí truyền dữ liệu và lưu trữ khác nhau theo vùng
- **Dịch Vụ và Tính Năng:** Tính khả dụng của các dịch vụ AWS cần thiết
- **Khôi Phục Thảm Họa:** Tách biệt địa lý để giảm thiểu rủi ro

Trong bài lab này, chúng ta sẽ chọn vùng đích dựa chủ yếu trên **tối ưu hóa chi phí** đồng thời duy trì sự tách biệt địa lý đầy đủ.

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
