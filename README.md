# Golden Jackets Chile 🧥🇬🇧

Community of AWS professionals who hold all 12 active AWS certifications — the Golden Jacket holders of the Chile.

## Website

[goldenjackets.cl](https://goldenjackets.cl)

## Structure

```
├── index.html          # Main site (members, events, articles, apply form)
├── members.html        # Members Lounge (authenticated)
├── admin.html          # Admin Console (chapter leader)
├── config.js           # Chapter configuration
├── assets/
│   ├── members/        # Member photos
│   ├── partners/       # Partner logos
│   ├── badges/         # AWS certification badges
│   └── *.png / *.jpg   # Site assets
├── .github/
│   └── workflows/
│       ├── deploy.yml          # S3 deploy + CloudFront invalidation
│       ├── deploy-staging.yml  # Staging deploy
│       └── create-user.yml     # User onboarding automation
├── SECURITY.md
└── README.md
```

## CI/CD

### Deploy (`deploy.yml`)
- Triggers on push to `master`
- Auto-numbers member cards
- Syncs to S3 bucket (`goldenjackets.cl`)
- Invalidates CloudFront cache
- Runs smoke tests

### User Onboarding (`create-user.yml`)
- Triggers on PR merge (new members)
- Creates Cognito user
- Sends welcome email

## Infrastructure

| Component | Value |
|-----------|-------|
| S3 Bucket | `goldenjackets.cl` |
| CloudFront | `E10YX1BT67IAVC` (`d245cwyl4dcv9y.cloudfront.net`) |
| Route 53 | `Z07759013CMW6IJZYOD7K` (hosted in account 958919067803) |
| ACM Certificate | `goldenjackets.cl` + `www.goldenjackets.cl` |
| Cognito Group | `chile` |
| Backup Vault | `gj-chile-backups` |
| AWS Account | `800712212925` (profile: gj) |

## Admin Features

- List/Create/Delete Cognito users
- Resend pending invitations
- Backup status + restore
- Export members CSV
- Community metrics
- Promote Challenger → Golden Jacket
- View project backlog

## Community

- **Website**: [goldenjackets.cl](https://goldenjackets.cl)
- **LinkedIn**: [Golden Jackets Chile](https://www.linkedin.com/company/golden-jackets-chile)

## Contributing

Members can submit articles and content through the Members Lounge.
For technical contributions, please open an issue or pull request.

---

*Independent community, not officially affiliated with Amazon Web Services.*
*Last updated: 17/05/2026*
