# Golden Jackets Chile 🧥🇨🇱

Community of AWS professionals who hold all 12 active AWS certifications — the Golden Jacket holders of Chile.

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
├── .kiro/
│   └── steering/       # AI development context (not deployed)
├── .github/
│   └── workflows/
│       ├── deploy.yml          # S3 deploy + CloudFront invalidation
│       ├── deploy-staging.yml  # Staging deploy
│       └── create-user.yml     # User onboarding automation
├── SECURITY.md
└── README.md
```

## Developer Tooling

| Tool | Purpose |
|------|---------|
| **Kiro CLI** | AI-assisted development (code, deploy, operations) |
| **MCP Server** | Custom tools for community management (list members, invalidate cache, chapter status) |
| **Steering Files** | AI context rules (conventions, security, infrastructure) — `.kiro/steering/` |
| **Knowledge Bases** | Indexed project history and architecture for cross-session context |

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
*Last updated: 25/05/2026*

## 🤖 Built With AI

This project was entirely built using **Kiro CLI** (powered by Claude, Anthropic) — from HTML/CSS/JS to AWS infrastructure, Lambda functions, CI/CD pipelines, and admin panel. Development is accelerated with MCP Server (custom tools), Steering Files (AI context), and Knowledge Bases (persistent memory).
