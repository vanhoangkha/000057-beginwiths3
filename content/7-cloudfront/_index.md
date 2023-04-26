---
title : "Accelerate Static Websites with Cloudfront"
date : "`r Sys.Date()`"
weight : 7
chapter : false
pre : " <b> 7. </b> "
---

#### Introduce

Congratulations on hosting a static website - successfully on Amazon S3 service, but need to make your S3 public! So how to host a Static Website on Amazon S3 without publicizing any information about your bucket?

This lab will walk you through the steps to host static web content in [Amazon S3 bucket](https://aws.amazon.com/s3/) , protected and accelerated by [Amazon CloudFront](https://aws.amazon.com/cloudfront/) . The skills learned will help you ensure your workloads are aligned with the [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc).

![example](/images/cf/s3_user.png?width=50pc)

#### Expense

- Usually less than $1 per month (depending on the number of requests)
- [Amazon S3Price](https://aws.amazon.com/s3/pricing/)
- [Amazon CloudFront Pricing](https://aws.amazon.com/cloudfront/pricing/)
- [Amazon Price](https://aws.amazon.com/pricing/)

#### References

- [Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)

#### Steps to take

1. [Block all public access to S3](7.1-block_all_public_access/)
2. [ConfigAmazon CloudFront](7.2-configuration_amazon_cloudfront/)
3. [Test CloudFront](7.3-test_cloudfront/)