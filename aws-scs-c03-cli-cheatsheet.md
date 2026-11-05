# AWS Certified Security – Specialty (SCS-C03) — CLI & Incident Runbook 🛡️☁️

A practical compilation of everyday AWS CLI security, audit, threat remediation, and governance commands mapped to the SCS-C03 exam curriculum. Curated by **EvolveSkill**.

---

## 1. Identity & Access Management (IAM) Security

Audit IAM credentials and generate reports:
> `aws iam get-credential-report`

List IAM policies with administrator permissions:
> `aws iam list-policies --scope Local --only-attached`

Enforce strong IAM account password policy:
> `aws iam update-account-password-policy --minimum-password-length 14 --require-symbols --require-numbers --require-uppercase-characters --require-lowercase-characters --allow-users-to-change-password`

Deactivate an exposed access key immediately:
> `aws iam update-access-key --access-key-id AKIAIOSFODNN7EXAMPLE --status Inactive --user-name SecurityAdmin`

---

## 2. Amazon S3 Storage Security & Access Control

Enable default S3 bucket encryption with AWS KMS:
> `aws s3api put-bucket-encryption --bucket evolveskill-secure-vault --server-side-encryption-configuration '{"Rules": [{"ApplyServerSideEncryptionByDefault": {"SSEAlgorithm": "aws:kms", "KMSMasterKeyId": "alias/aws/s3"}}]}'`

Block all public access at the bucket level:
> `aws s3api put-public-access-block --bucket evolveskill-secure-vault --public-access-block-configuration "BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true"`

Enable bucket versioning for ransomware protection:
> `aws s3api put-bucket-versioning --bucket evolveskill-secure-vault --versioning-configuration Status=Enabled`

---

## 3. Threat Detection & Security Monitoring

Enable Amazon GuardDuty detector in the current region:
> `aws guardduty create-detector --enable`

List high-severity GuardDuty security findings:
> `aws guardduty list-findings --detector-id 12abc34d567e8fa9012bc34d567e8fa0 --finding-criteria '{"Criterion": {"severity": {"Gte": 7}}}'`

Enable AWS Security Hub across all standards:
> `aws securityhub enable-security-hub --enable-default-standards`

---

## 4. Logging & Governance (CloudTrail & AWS Config)

Create an encrypted multi-region CloudTrail trail:
> `aws cloudtrail create-trail --name sec-mgmt-trail --s3-bucket-name evolveskill-cloudtrail-logs --is-multi-region-trail --enable-log-file-validation`

Start logging on the CloudTrail trail:
> `aws cloudtrail start-logging --name sec-mgmt-trail`

Start AWS Config recording for compliance tracking:
> `aws configservice start-configuration-recorder --configuration-recorder-name default`

---

## 5. Network Security & Key Management (KMS)

Enable AWS KMS key rotation:
> `aws kms enable-key-rotation --key-id 1234abcd-12ab-34cd-56ef-1234567890ab`

Revoke an overly permissive Security Group ingress rule (SSH port 22 open to world):
> `aws ec2 revoke-security-group-ingress --group-id sg-0123456789abcdef0 --protocol tcp --port 22 --cidr 0.0.0.0/0`

Associate AWS WAF Web ACL with an Application Load Balancer:
> `aws wafv2 associate-web-acl --web-acl-arn arn:aws:wafv2:us-east-1:123456789012:regional/webacl/EvolveSkillWAF/abc123 --resource-arn arn:aws:elasticloadbalancing:us-east-1:123456789012:loadbalancer/app/prod-alb/1234567890`

---

## 📚 Study Notes & Certification Track
- Full SCS-C03 Study Blueprints: [evolveskill4.com](https://evolveskill4.com)
- Practical Cloud Security Labs: [EvolveSkill Substack](https://substack.com/@evolveskill4)

---
*Documented by Rahul Sharma | Technical Content Writer @ EvolveSkill*
