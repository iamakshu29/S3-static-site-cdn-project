step-by-step manual hands-on notes for the Static Website Hosting Project using S3 + CloudFront + Route 53 — formatted for documentation or GitHub README.

📘 Manual Hands-On Notes: Static Website Hosting on AWS
Project Name: Static Website with CDN and Custom Domain
Services Used: S3, CloudFront, Route 53, IAM, ACM

🪣 Step 1: Create and Configure S3 Bucket
Go to S3 → Create Bucket

Name: your-bucket-name

Region: (any)

Uncheck "Block all public access"

Enable Versioning (optional but good practice)

Upload Files

Upload index.html, CSS, JS, images

Enable Static Website Hosting

Go to Properties → Static Website Hosting

Enable

Set:

Index document: index.html

Error document: 404.html (optional)

Set Bucket Policy (for public access or CloudFront OAC)
(Public access example:)
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}



🌍 Step 2: Setup CloudFront CDN
Create Distribution → Web (CloudFront)

Origin Domain: Choose your S3 bucket (without website endpoint)

Origin Access: Create Origin Access Control (OAC) and attach policy

Viewer Protocol Policy: Redirect HTTP to HTTPS

Cache Policy: Use default (or modify if needed)

Default Root Object: index.html

Price Class: Use Only US, Canada, and Europe (or broader)

Alternate Domain Name (CNAME): Add www.yourdomain.com (optional — see Route 53)

SSL Certificate: Choose ACM certificate for your domain (must be in us-east-1)

Wait ~10–15 minutes for distribution to deploy

Test CloudFront Domain
Visit:
https://<distribution-id>.cloudfront.net/index.html


📛 Step 3: Route 53 – Map Custom Domain
Create or use existing Hosted Zone for yourdomain.com

Create Record (Alias)

Type: A

Name: www (or leave blank for root domain)

Alias → Yes

Target: Select CloudFront distribution

Test Custom Domain
Visit:
https://www.yourdomain.com
🔐 Step 4: SSL Certificate with ACM
Go to ACM (in us-east-1)

Request Public Certificate

Add:

www.yourdomain.com

yourdomain.com (optional)

Choose DNS validation

Add Validation Record in Route 53

ACM gives you a CNAME to add

Go to Route 53 → Hosted Zone → Create record

Paste the ACM CNAME

Wait for validation
After it’s "Issued", you can attach it to CloudFront

🧹 Step 5: Cleanup (To Avoid Charges)
To avoid monthly AWS billing:

❌ Delete the S3 bucket (after backing up)

❌ Disable and delete the CloudFront distribution

❌ Delete the Route 53 Hosted Zone (or records if domain stays)

❌ Cancel domain auto-renew (optional)

❌ Remove ACM certificate (optional)

