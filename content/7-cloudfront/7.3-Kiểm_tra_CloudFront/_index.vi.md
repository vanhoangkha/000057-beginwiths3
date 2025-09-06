---
title: "Kiểm tra Amazon CloudFront"
date: "2025-09-06"
weight: 3
chapter: false
pre: "<b> 7.3 </b>"
---

#### 1. Kiểm tra CloudFront

- Trong giao diện CloudFront, chọn **ID**.

  ![CF](/images/cf/7.3/0001.png?featherlight=false&width=90pc)

- Tại mục **Distribution domain name**:
  - Đảm bảo rằng CloudFront đã deploy xong bằng cách xem nội dung ở mục **Last modified**.
  - Chọn ký hiệu **ô vuông** để copy URL.

  ![CF](/images/cf/7.3/0002.png?featherlight=false&width=90pc)

- Bật một tab khác và dán giá trị CloudFront URL vào thanh tìm kiếm rồi nhấn enter.

  ![CF](/images/cf/7.3/0003.png?featherlight=false&width=90pc)

- Chúc mừng bạn đã triển khai thành công CloudFront để phân phối một website tĩnh được host trên S3 mà không cần phải public bucket hay object.

#### 2. Kiểm tra thời gian load website

- Trong bước 6 (kiểm tra website), bạn đã thấy rằng với chức năng **Static website hosting** của S3, trang web du lịch cần khoảng 0.614 giây để load website. Hãy xem dịch vụ CloudFront đã giúp giảm thời gian này còn bao nhiêu.

- Tại giao diện website về du lịch, nhấp chuột phải và chọn **Inspect**.

  ![CF](/images/cf/7.3/0004.png?featherlight=false&width=90pc)

- Phía trên cùng bên phải, chọn **Network**.
- Phía trên cùng bên trái, chọn biểu tượng **reload**.

  ![CF](/images/cf/7.3/0005.png?featherlight=false&width=90pc)

- Tại mục URL của **Distribution domain name**, bạn sẽ thấy cột thời gian hiển thị giá trị là 13 ms (milliseconds) = 0.013 giây (lưu ý: giá trị này chỉ mang tính tương đối, tùy thuộc từng thời điểm - thời gian này sẽ tăng hoặc giảm).

  ![CF](/images/cf/7.3/0007.png?featherlight=false&width=90pc)

- Kiểm tra xem nội dung của website này đang được trả về từ PoP nào trong 450+ Points of Presence (PoP) trên toàn cầu.
    - Nhấp vào **Distribution domain name**.
    - Chọn tab **Headers**.
    - Xem **x-amz-cf-pop**, với giá trị **SGN50-P1** là [Ho Chi Minh City](https://www.feitsui.com/en/article/3).

  ![CF](/images/cf/7.3/0008'.png?featherlight=false&width=90pc)

- Nếu bạn đang ở Hà Nội và thực hiện bài lab này, nội dung Website sẽ trả về từ PoP tại Hà Nội, nơi mà AWS vừa triển khai trong [năm 2022](https://aws.amazon.com/about-aws/whats-new/2022/08/aws-new-edge-locations-vietnam/).

#### 3. Tóm tắt

- Qua bài lab này, bạn đã thấy được hai tiện ích tuyệt vời của CloudFront:
  - Phân phối nội dung của một website tĩnh được host trên S3 mà không cần phải public bucket hay object, tăng tính bảo mật.
  - Phân phối nội dung với độ trễ thấp và tốc độ truyền nhanh chóng, cải thiện latency bằng cách CloudFront lấy nội dung ở Edge location gần với địa điểm của khách hàng nhất.

- Dù trong bài lab này, độ trễ khá thấp - chỉ ở mức milliseconds, nhưng trong thực tế, với các website có lượng thông tin lớn hơn, CloudFront là giải pháp giúp end users truy cập nhanh chóng vào trang web, góp phần đảm bảo trải nghiệm tốt đẹp của người dùng cuối.
