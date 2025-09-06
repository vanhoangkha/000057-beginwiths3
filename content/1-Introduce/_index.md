---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Overview

Amazon Simple Storage Service (Amazon S3) is an object storage service that provides on-demand scalability, ensuring high levels of data availability, security, and performance. S3 is designed to deliver 99.999999999% (11 9's) durability and stores data for millions of applications worldwide.

#### What is Amazon S3?

Amazon S3 is a web service that offers industry-leading scalability, data availability, security, and performance. S3 stores data as objects within buckets, where each object can range from 0 bytes to 5 TB in size. With virtually unlimited storage capacity, S3 can handle any amount of data from anywhere on the web.

#### Understanding S3 Buckets vs Objects

Before diving into the lab, it's crucial to understand the fundamental difference between S3 Buckets and Objects:

**S3 Bucket:**
- **What it is**: A top-level container that holds your objects
- **Naming**: Must be **globally unique** across all AWS accounts worldwide
- **Location**: Exists in a specific AWS Region
- **Limit**: Maximum 100 buckets per AWS account (can be increased)
- **Function**: 
  - Organizes and groups objects
  - Applies policies and permissions
  - Configures features (versioning, encryption, logging)
  - Defines access controls

**Example bucket name**: `my-website-bucket-2024`

**S3 Object:**
- **What it is**: The actual files/data stored inside a bucket
- **Naming**: Key name, only needs to be unique **within that bucket**
- **Size**: From 0 bytes to 5TB per object
- **Limit**: Unlimited objects per bucket
- **Function**:
  - Contains actual data (HTML, images, videos, documents)
  - Has its own metadata
  - Can have individual permissions (with ACLs)

**Example object keys**: `images/logo.png`, `index.html`, `css/style.css`

**Relationship Structure:**
```
Bucket: my-website-bucket
├── index.html (Object)
├── about.html (Object)  
├── css/
│   └── style.css (Object)
└── images/
    ├── logo.png (Object)
    └── banner.jpg (Object)
```

**Simple Analogy:**
- **Bucket** = Filing cabinet
- **Object** = Documents inside the cabinet

**URL Structure:**
- **Bucket**: `https://my-bucket.s3.amazonaws.com/`
- **Object**: `https://my-bucket.s3.amazonaws.com/folder/file.jpg`

**Permission Levels:**
- **Bucket-level**: Controls who can access the bucket itself
- **Object-level**: Controls who can access specific objects

**Summary**: A bucket is the "container," and objects are the "content" inside that container.

#### Key Features

**Storage Classes:**
- **S3 Standard:** For frequently accessed data with low latency and high throughput
- **S3 Intelligent-Tiering:** Automatically moves data between access tiers to optimize costs
- **S3 Standard-IA:** For infrequently accessed data with rapid access when needed
- **S3 Glacier:** For long-term archival with retrieval times from minutes to hours
- **S3 Glacier Deep Archive:** Lowest-cost storage for long-term retention

**Security & Compliance:**
- Encryption in transit and at rest (SSE-S3, SSE-KMS, SSE-C)
- Access control through IAM policies, bucket policies, and ACLs
- AWS CloudTrail for API logging and monitoring
- Compliance with SOC, PCI, HIPAA, and other standards

**Management & Analytics:**
- **Versioning:** Keep multiple versions of objects for data protection
- **Cross-Region Replication:** Automatically replicate data across AWS regions
- **Lifecycle Management:** Automatically transition objects between storage classes
- **S3 Storage Lens:** Organization-wide visibility into storage usage and costs

**Performance & Availability:**
- 99.99% availability SLA for S3 Standard
- Request rates of 3,500 PUT/COPY/POST/DELETE and 5,500 GET/HEAD requests per second per prefix
- Transfer Acceleration using CloudFront edge locations
- Multipart upload for large objects

#### Common Use Cases

S3 serves a wide variety of use cases across industries:

- **Data Lakes & Analytics:** Store structured and unstructured data for big data analytics
- **Backup & Restore:** Reliable backup solution with cross-region replication
- **Content Distribution:** Static website hosting and content delivery
- **Data Archiving:** Long-term retention with Glacier storage classes
- **Disaster Recovery:** Geographic redundancy for business continuity
- **Application Data Storage:** Scalable storage for mobile and web applications
- **Media & Entertainment:** Store and distribute video, audio, and image content

#### Benefits

- **Scalability:** Virtually unlimited storage capacity that grows with your needs
- **Durability:** 99.999999999% (11 9's) durability protects against data loss
- **Cost-Effective:** Pay only for what you use with multiple pricing tiers
- **Security:** Enterprise-grade security with multiple encryption options
- **Integration:** Seamless integration with other AWS services
- **Global Accessibility:** Access your data from anywhere in the world

![S3](/images/icon.png?featherlight=false&width=10pc)
