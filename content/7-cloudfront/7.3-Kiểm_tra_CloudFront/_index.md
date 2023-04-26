---
title : "Test Amazon Cloudfront"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 7.3 </b> "
---

1. Check **CloudFront**

- In the CloudFront interface, select **ID**

![CF](/images/cf/7.3/0001.png?featherlight=false&width=90pc)

- In the **Distribution domain name** section:
     - Make sure that CloudFront has been deployed by looking at the content in the **Last modified** section
     - Select the **square** symbol to copy the URL

![CF](/images/cf/7.3/0002.png?featherlight=false&width=90pc)

- Open another tab and paste the CloudFront URl value in the search bar then press enter

![CF](/images/cf/7.3/0003.png?featherlight=false&width=90pc)

-> Congratulations on successfully deploying Cloudfront to deliver a static website hosted on S3 without requirement for public buckets or objects

2. Check website load time

- In step 6 (website check), you have seen that: with **Static website hosting** function of S3 - travel website needs about 0.614 seconds to load website! So let's see how many seconds the CLoudFront service has reduced this time.

- At the website interface about tourism, right-click and select **Inspect**

![CF](/images/cf/7.3/0004.png?featherlight=false&width=90pc)

- On the top right, select **Netword**
- At the top left, select the **reload** icon

![CF](/images/cf/7.3/0005.png?featherlight=false&width=90pc)

- At the URL section of **Distribution domain name**, you will see that the time column displays a value of 13 ms (milliseconds) = 0.013 seconds (note: this value is only approximate, depending on each time - this time will increase or decrease)

![CF](/images/cf/7.3/0007.png?featherlight=false&width=90pc)

- Check the content of this website is being returned from which PoP in 450+ Points of Presence (PoP) globally
     - Click **Distribution domain name**
     - Select tab **Headers**
     - See **x-amz-cf-pop**, with value **SGN50-P1** as [Ho Chi Minh City](https://www.feitsui.com/en/article/3)

![CF](/images/cf/7.3/0008'.png?featherlight=false&width=90pc)

- If you are in Hanoi and doing this lab, the Website content will return from the PoP in Ha Noi where AWS has just deployed in [2022](https://aws.amazon.com/about-aws/whats-new/2022/08/aws-new-edge-locations-vietnam/)

3. Summary

- Through this lab you have seen 2 great utilities of CloudFront:

     - Distribute the content of a static website hosted on S3 without requirement for Public Bucket or Object -> **Increase security**
     - Deliver content securely with low latency and fast transfer speeds -> **improved Latency** by CloudFront will get content at the Edge location closest to the customer's location.

         - Although in this lab, the latency is quite low - only milliseconds! But in reality, for websites with a larger amount of information, CloudFront is the solution to help EndUsers quickly access the website, contributing to ensuring a great experience for the end user.