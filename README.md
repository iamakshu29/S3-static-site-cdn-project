# Static Website Hosting on AWS (S3 + CloudFront + Route 53)

This project demonstrates a real-world static website deployment on AWS using:

- **Amazon S3** for website file hosting
- **Amazon CloudFront** as CDN to cache content globally
- **Amazon Route 53** for custom domain and DNS routing
- **IAM** for bucket access policies and security

## 🧰 Services Used
- S3
- CloudFront
- Route 53
- IAM
- ACM (for SSL certificate)

## 🧠 Skills Learned
- Static website hosting on S3
- CDN caching with CloudFront
- DNS and custom domain setup via Route 53
- Configuring public access + bucket policies
- HTTPS via ACM certificates

## 💡 Architecture
[Add architecture diagram or explain steps here]

## ⚙️ Cleanup Notes
All AWS resources were deleted to avoid ongoing charges. This repository contains all the source code and architecture for future redeployment.

## 🚀 How to Re-Deploy
Instructions for recreating the setup:
1. Create S3 bucket and upload files
2. Configure static website hosting
3. Set up CloudFront distribution
4. Request and validate SSL via ACM (in us-east-1)
5. Map domain using Route 53 with Alias records
