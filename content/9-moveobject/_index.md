---
title: "Move obejcts"
date: "`r Sys.Date()`"
weight: 9
chapter: false
pre: " <b> 9. </b> "
---

#### Move Objects

- With the move action in the S3 console, you can move an object to a folder (prefix) in the same bucket, to another bucket/prefix

![Static website](/images/8-moveobject/0000.png?featherlight=false&width=50pc)

1. Next we will create a new **bucket**

   - In the **S3 bucket** console, select **Create bucket**

   ![Static website](/images/8-moveobject/0001.png?featherlight=false&width=90pc)

   - In the **Bucket name** field, enter `aws-first-cloud-journey-move`
   - In the **AWS region** section, select **Asia Pacific (Singapore) ap-southeast-1** as the region with the closest geographical distance to Vietnam users as of September 2023

   ![Static website](/images/8-moveobject/0002.png?featherlight=false&width=90pc)

   - Keep the default values, scroll to the bottom of the page, select `Create bucket`

   ![Static website](/images/8-moveobject/0003.png?featherlight=false&width=90pc)

2. Move files between **Buckets**

   - In the **Amazon S3** console, select bucket **aws-first-cloud-journey**

   ![Static website](/images/8-moveobject/0004.png?featherlight=false&width=90pc)

   - Check the **square** symbol next to the **Name** value to select all Objects in the bucket

   - Select **Action**, select **Calculate total size**

   ![Static website](/images/8-moveobject/0005''.png?featherlight=false&width=90pc)

   - **Result**: you have a total of 182 objects corresponding to 21.2 MB, select **Close** to go back

   ![Static website](/images/8-moveobject/0005'.png?featherlight=false&width=90pc)

   - Check the **square** symbol next to the **Name** value to select all Objects in the bucket

   - Select **Action**, select **Move**

   ![Static website](/images/8-moveobject/0005.png?featherlight=false&width=90pc)

   - Scroll down the middle of the page, in the **Destination type** section, select **Bucket**, select **Browse S3**

   ![Static website](/images/8-moveobject/0006.png?featherlight=false&width=90pc)

   - Select **S3 Buckets**

   ![Static website](/images/8-moveobject/0007.png?featherlight=false&width=90pc)

   - Select bucket name **aws-first-cloud-journey-move**, select **Choose destination**

   ![Static website](/images/8-moveobject/0008.png?featherlight=false&width=90pc)

   - Scroll to the bottom of the page, in the **Additional checksums** section keep the default **Copy existing checksum functions**, select **Move**

   - **Noted**: Amazon S3 uses **checksum** to verify the integrity of the data you upload, download, or copy your data from S3

   ![Static website](/images/8-moveobject/0009.png?featherlight=false&width=90pc)

   - Congratulations, you have successfully moved the file, select **Close**

   ![Static website](/images/8-moveobject/00010.png?featherlight=false&width=90pc)

3. Check the Object in the new Bucket

   - In the **Amazon S3** console, select bucket name **aws-first-cloud-journey-move**

   ![Static website](/images/8-moveobject/00011.png?featherlight=false&width=90pc)

   - Check the **square** symbol next to the **Name** value to select all Objects in the bucket

   - Select **Action**, select **Calculate total size**

   ![Static website](/images/8-moveobject/00012.png?featherlight=false&width=90pc)

   - **Result**: you have a total of 182 objects corresponding to 21.2 MB -> similar to the calculation of the total size of the bucket **aws-first-cloud-journey**

   ![Static website](/images/8-moveobject/00013.png?featherlight=false&width=90pc)
