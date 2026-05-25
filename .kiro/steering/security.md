# Security

## When to Apply
When editing authentication, API calls, or member data.

## Rules
- Cognito User Pool handles all authentication — never implement custom auth
- Admin actions require email in ADMIN_EMAILS list (defined in config.js)
- Never expose AWS credentials or account IDs in client-side code
- All API calls go through API Gateway with rate limiting
- Privacy compliance required: privacy consent before processing personal data
- Member data (emails, names) must never be committed to the repository
- MFA available for admin accounts via TOTP
- Tokens stored in sessionStorage (not localStorage) for session-scoped access
- Auto-refresh token logic handles expired sessions transparently
