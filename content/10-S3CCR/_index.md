---
title: "Replication Object multi Region"
date: "2025-09-06"
weight: 10
chapter: false
pre: " <b> 10. </b> "
---

#### Amazon S3 Cross-Region Replication (CRR)

#### What is Cross-Region Replication?

Amazon S3 Cross-Region Replication (CRR) is a feature that automatically replicates objects across buckets in different AWS regions. This provides geographic redundancy and helps meet compliance requirements while improving data availability and disaster recovery capabilities.

#### Key Benefits

- **Disaster Recovery:** Protect against regional outages and disasters
- **Compliance:** Meet regulatory requirements for geographic data distribution
- **Latency Reduction:** Serve content from regions closer to users
- **Data Sovereignty:** Keep copies of data in specific geographic locations
- **Operational Excellence:** Maintain business continuity across regions

#### How CRR Works

When CRR is configured:
- Objects are automatically copied to destination buckets in different regions
- Replication occurs asynchronously, typically within 15 minutes
- Object metadata, ACLs, and tags are preserved during replication
- Versioning must be enabled on both source and destination buckets
- IAM roles provide necessary permissions for the replication process

#### AWS Well-Architected Framework

[AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) helps you build secure, high-performing, resilient, and efficient infrastructure. Based on 6 main pillars, with the **Reliability** pillar being the focus of this lab.

To ensure the **Reliability** of the system, objects stored in the S3 bucket in Singapore Region (ap-southeast-1) should be **replicated** to another region for redundancy and disaster recovery.

![Static website](/images/10-s3crr/0000.png?featherlight=false&width=50pc)

#### Region Selection Criteria

When choosing a destination region for replication, consider these factors:

- **Compliance:** Regulatory requirements for data location
- **Latency:** Distance to end users for performance optimization
- **Cost:** Data transfer and storage costs vary by region
- **Services and Features:** Availability of required AWS services
- **Disaster Recovery:** Geographic separation for risk mitigation

For this lab, we will select the destination region based primarily on **cost optimization** while maintaining adequate geographic separation.

- -> So Region N. Virginia (us-east-1) with S3 cost: 23.55 USD for 1TB per month - 2.05 USD cheaper than Region Singapore (ap-southeast-1) is a suitable choice for the criteria **Cost**. You can double check the cost at the official page of [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=71e120e9a6a9ffe41d37144b4e2c92537b88eb58)

![Static website](/images/10-s3crr/0001.png?featherlight=false&width=90pc)


1. Next we will create a new **buecket**

   - In the **S3 bucket** interface, select **Create bucket**

   ![Static website](/images/10-s3crr/0002'.png?featherlight=false&width=90pc)

   - In the **Bucket name** field, type ``aws-first-cloud-journey-cross``
   - In the **AWS region** section, select **US East (N. Virginia) us-east-1**

   ![Static website](/images/10-s3crr/0002.png?featherlight=false&width=90pc)

   - Keep the default values, scroll to the bottom of the page, select ``Create bucket``

   ![Static website](/images/10-s3crr/0003.png?featherlight=false&width=90pc)

2. Replicate files between **Buckets** in different Regions

   - In the **Amazon S3** interface, select bucket **aws-first-cloud-journey**

   ![Static website](/images/10-s3crr/0004.png?featherlight=false&width=90pc)

   - Select **Management**

   ![Static website](/images/10-s3crr/0005.png?featherlight=false&width=90pc)

   - Scroll down to the middle of the page, select **Create replication rule**

   ![Static website](/images/10-s3crr/0006.png?featherlight=false&width=90pc)

   - In the Replication rule name section, enter ``PrimaryToSecondary``
   - In Status section, keep **Enabled**
   - In the Choose a rule scope section, select **Apply to all objects in the bucket**, which means this config will be applied to all objects in the bucket.
   - In the Destination section, select **Choose a bucket in this account**
      - **Note:** As you can see, we can choose the function **Specify a bucket in another account** which means copying data to a bucket belonging to another AWS account, however within the framework of this lab, We just choose the solution of copying data to another bucket but still in the current AWS account.
   - In the Bucket name section, select **Browse S3**

   ![Static website](/images/10-s3crr/0007.png?featherlight=false&width=90pc)

   - Check the circle symbol to select Bucket: **aws-first-cloud-journey-cross**, select **Choose path**

   ![Static website](/images/10-s3crr/0008.png?featherlight=false&width=90pc)

   - At this time, the Amazon S3 service requires you to enable the **versioning** feature to continue configuration. You can review the lab **8. BUCKET VERSIONING** to understand this concept further.

   - Select **Enable bucket versioning**

   ![Static website](/images/10-s3crr/0009.png?featherlight=false&width=90pc)

   - In the IAM role section, keep the default **Choose from existing IAM roles**
   - Select the triangle symbol -> the value table appears -> select **Create new role**

   ![Static website](/images/10-s3crr/00010.png?featherlight=false&width=90pc)
    
   - Keep the remaining default values. 
   - Scroll to the bottom of the page in the Additional replication options section, select **Replication Time Control (RTC)**, which 3 RTC replicates most objects that you upload to Amazon S3 in seconds, and 99.99 percent of those objects within 15 minutes
   - Select **Save**

   ![Static website](/images/10-s3crr/00011.png?featherlight=false&width=90pc)

   - In the section, Replicate existing objects?, select **No, do not replicate existing objects.**, which means only start copying newly uploaded objects to Bucket in region Singapore via Bucket in region N.Virginia

   ![Static website](/images/10-s3crr/00012.png?featherlight=false&width=90pc)

3. Check S3 bucket **aws-first-cloud-journey-cross**

   - In the interface, S3 bucket **aws-first-cloud-journey-cross** in region N. Virginia, you can see that there are no objects in this bucket yet

   ![Static website](/images/10-s3crr/00013.png?featherlight=false&width=90pc)

4. Upload new file to S3 bucket **AWS First Cloud Journey**

   - At the S3 bucket interface **AWS First Cloud Journey**, select **Upload**

   - Open the window containing the **folders**, **files** downloaded and extracted in [step 2.2](https://000057.awsstudygroup.com/2-prerequiste/2.2-uploaddata/)

   - Select the **images** folder -> choose any photo -> upload to the **AWS First Cloud Journey** bucket by dragging and dropping

   ![Static website](/images/10-s3crr/00014.png?featherlight=false&width=90pc)

   - At the **Upload** interface, in the **Files and folders** section, the blog-3.jpg file appears, scroll to the bottom of the page and select **Upload**

   ![Static website](/images/10-s3crr/00015.png?featherlight=false&width=90pc)

   - The **upload** file has been completed, select **Close** to return to the **bucket** interface

   ![Static website](/images/10-s3crr/00016.png?featherlight=false&width=90pc)
   
5. Check the **Replication** feature

   - In the S3 interface, select bucket **aws-first-cloud-journey-cross** in region N. Virginia

   ![Static website](/images/10-s3crr/00017.png?featherlight=false&width=90pc)

   - Check Object

   - **Noted**: If the Object has not appeared, please be patient for a few minutes and refresh the page

   ![Static website](/images/10-s3crr/00018.png?featherlight=false&width=90pc)

   - -> An Object has appeared

   - Select the square symbol in front of the object **blog-3.jpg**, select **Open**

   ![Static website](/images/10-s3crr/00019.png?featherlight=false&width=90pc)

   - Result:

   ![Static website](/images/10-s3crr/00020.png?featherlight=false&width=90pc)

   - -> Similar to the image file you uploaded to S3 bucket **AWS First Cloud Journey** in step 4

   - => Congratulations on completing the object replication lab between S3 buckets in 2 different Regions