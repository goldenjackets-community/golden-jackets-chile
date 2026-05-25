# Infrastructure

## When to Apply
When discussing deploy, CI/CD, or AWS resources.

## Rules
- Hosted on S3 (static website) behind CloudFront with WAF
- Region: us-east-1
- Deploy via GitHub Actions (`deploy.yml`) — never manual S3 sync
- CI/CD auto-numbers member cards and invalidates CloudFront cache
- WAF protects with rate limiting and bot control
- Budget alarm at $10/month — always keep costs minimal
- Prefer serverless (Lambda, DynamoDB, API Gateway) over always-on resources
- Backups managed by AWS Backup (daily/weekly/monthly)
- Default branch is `master`
