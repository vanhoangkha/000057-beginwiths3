---
title: "Notes & Best Practices"
date: "2025-09-06"
weight: 12
chapter: false
pre: " <b> 12. </b> "
---

#### AWS S3 Best Practices & Troubleshooting Guide

#### Security Best Practices

#### 1. Block Public Access
- **Always keep Block Public Access enabled** in production
- Use CloudFront with Origin Access Control (OAC) instead of public buckets
- Never disable all four Block Public Access settings unless absolutely necessary

#### 2. Bucket Policies
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudFrontServicePrincipal",
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::account-id:distribution/distribution-id"
        }
      }
    }
  ]
}
```

#### 3. Encryption
- Enable default encryption (SSE-S3 or SSE-KMS)
- Use SSE-KMS for sensitive data with proper key policies
- Consider client-side encryption for highly sensitive data

#### Performance Best Practices

#### 1. CloudFront Configuration
- Use Origin Access Control (OAC) instead of Origin Access Identity (OAI)
- Configure appropriate cache behaviors and TTL values
- Enable compression for text-based content
- Use HTTP/2 and IPv6 support

#### 2. S3 Transfer Acceleration
- Enable for global uploads/downloads
- Use multipart upload for files > 100MB
- Implement retry logic with exponential backoff

#### 3. Request Patterns
- Avoid sequential key names (use random prefixes)
- Distribute requests across multiple prefixes
- Use S3 Transfer Acceleration for global access

#### Cost Optimization

#### 1. Storage Classes
- Use S3 Intelligent-Tiering for unknown access patterns
- Implement lifecycle policies to transition to cheaper storage classes
- Use S3 Storage Lens for cost analysis

#### 2. Versioning Management
```json
{
  "Rules": [
    {
      "ID": "DeleteOldVersions",
      "Status": "Enabled",
      "NoncurrentVersionExpiration": {
        "NoncurrentDays": 30
      }
    }
  ]
}
```

#### 3. Data Transfer
- Use CloudFront to reduce data transfer costs
- Consider S3 Transfer Acceleration pricing vs standard transfer
- Monitor CloudWatch metrics for optimization opportunities

#### Common Issues & Troubleshooting

#### 1. 403 Forbidden Errors
**Symptoms:** Cannot access S3 objects through CloudFront
**Causes:**
- Block Public Access is enabled but no proper OAC setup
- Incorrect bucket policy
- Missing CloudFront permissions

**Solutions:**
```bash
# Check bucket policy
aws s3api get-bucket-policy --bucket your-bucket-name

# Verify CloudFront OAC configuration
aws cloudfront get-origin-access-control --id your-oac-id

# Update bucket policy for OAC
aws s3api put-bucket-policy --bucket your-bucket-name --policy file://policy.json
```

#### 2. Website Endpoint vs Bucket Endpoint
**Issue:** Confusion between S3 website endpoint and bucket endpoint

**S3 Website Endpoint:**
- Format: `bucket-name.s3-website-region.amazonaws.com`
- Supports index/error documents
- Cannot use OAC/OAI
- Must use as CloudFront custom origin

**S3 Bucket Endpoint:**
- Format: `bucket-name.s3.region.amazonaws.com`
- Supports OAC/OAI
- Better security
- Recommended for CloudFront

#### 3. CORS Issues
**Symptoms:** Browser blocks requests from web applications
**Solution:**
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["GET", "HEAD"],
    "AllowedOrigins": ["https://yourdomain.com"],
    "ExposeHeaders": ["ETag"],
    "MaxAgeSeconds": 3000
  }
]
```

#### 4. Versioning Costs
**Issue:** Unexpected high storage costs
**Monitoring:**
```bash
# List object versions
aws s3api list-object-versions --bucket your-bucket-name

# Check storage metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/S3 \
  --metric-name BucketSizeBytes \
  --dimensions Name=BucketName,Value=your-bucket-name \
  --start-time 2024-01-01T00:00:00Z \
  --end-time 2024-01-31T23:59:59Z \
  --period 86400 \
  --statistics Average
```

#### Recommended Resources

#### Official AWS Documentation
- [S3 User Guide](https://docs.aws.amazon.com/AmazonS3/latest/userguide/)
- [CloudFront Developer Guide](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/)
- [S3 Security Best Practices](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)

#### AWS Blogs & Whitepapers
- [Amazon S3 Security Best Practices](https://aws.amazon.com/blogs/aws/amazon-s3-security-best-practices/)
- [Optimizing Amazon S3 Performance](https://aws.amazon.com/blogs/aws/amazon-s3-performance-tips-tricks/)
- [AWS Well-Architected Framework](https://aws.amazon.com/architecture/well-architected/)

#### Tools & Services
- **AWS Config:** Monitor S3 bucket compliance
- **AWS CloudTrail:** Audit S3 API calls
- **S3 Storage Lens:** Analyze storage usage and costs
- **AWS Trusted Advisor:** Get optimization recommendations

#### Useful CLI Commands

#### Bucket Management
```bash
# Create bucket with encryption
aws s3api create-bucket --bucket my-secure-bucket \
  --region us-east-1 \
  --create-bucket-configuration LocationConstraint=us-east-1

# Enable versioning
aws s3api put-bucket-versioning --bucket my-bucket \
  --versioning-configuration Status=Enabled

# Set lifecycle policy
aws s3api put-bucket-lifecycle-configuration --bucket my-bucket \
  --lifecycle-configuration file://lifecycle.json
```

#### Monitoring & Debugging
```bash
# Check bucket policy
aws s3api get-bucket-policy --bucket my-bucket

# List all versions of objects
aws s3api list-object-versions --bucket my-bucket

# Get bucket metrics
aws s3api get-bucket-metrics-configuration --bucket my-bucket \
  --id my-metrics-config
```

#### Production Checklist

Before deploying to production:

- [ ] Block Public Access is enabled
- [ ] CloudFront uses OAC (not OAI)
- [ ] Bucket policy follows least privilege principle
- [ ] Default encryption is enabled
- [ ] Lifecycle policies are configured
- [ ] Monitoring and alerting are set up
- [ ] Backup and disaster recovery plan exists
- [ ] Cost monitoring is configured
- [ ] Security scanning is implemented
- [ ] Access logging is enabled

#### Migration from Legacy Setup

If you're using the setup from this tutorial in production:

1. **Create new CloudFront distribution with OAC**
2. **Update DNS to point to new distribution**
3. **Test thoroughly before removing old setup**
4. **Enable Block Public Access**
5. **Update monitoring and alerting**

Remember: This tutorial is for learning purposes. Production environments require additional security and performance considerations.
