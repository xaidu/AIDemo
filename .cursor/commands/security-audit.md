# Security Audit

Comprehensive security review checklist for code and applications.

## Authentication & Authorization
- [ ] User authentication is properly implemented
- [ ] Session management is secure
- [ ] Password policies are enforced
- [ ] Multi-factor authentication considered
- [ ] Authorization checks are present and correct
- [ ] Role-based access control implemented properly
- [ ] JWT tokens are handled securely
- [ ] Account lockout mechanisms in place

## Input Validation & Sanitization
- [ ] All user inputs are validated
- [ ] Input sanitization prevents XSS
- [ ] SQL injection protection in place
- [ ] File upload security measures implemented
- [ ] URL parameter validation
- [ ] Form data validation
- [ ] API input validation
- [ ] Size limits on inputs enforced

## Data Protection
- [ ] Sensitive data is encrypted at rest
- [ ] Data in transit uses TLS/SSL
- [ ] Database connections are encrypted
- [ ] Personal information is properly protected
- [ ] Payment information follows PCI standards
- [ ] Data retention policies implemented
- [ ] Secure data deletion procedures
- [ ] Backup security measures

## Configuration & Infrastructure
- [ ] Environment variables for secrets
- [ ] No hardcoded credentials or keys
- [ ] Secure default configurations
- [ ] Unnecessary services/ports disabled
- [ ] Security headers implemented
- [ ] CORS policies properly configured
- [ ] Rate limiting in place
- [ ] Error messages don't leak information

## Dependencies & Third-Party
- [ ] Dependencies are up to date
- [ ] Known vulnerabilities addressed
- [ ] Third-party integrations are secure
- [ ] API keys are properly managed
- [ ] OAuth implementations are correct
- [ ] CDN and external resources secured
- [ ] Supply chain security considered

## Logging & Monitoring
- [ ] Security events are logged
- [ ] Log data doesn't contain sensitive info
- [ ] Failed login attempts monitored
- [ ] Unusual activity detection
- [ ] Log integrity protection
- [ ] Incident response procedures
- [ ] Audit trail maintenance

## Application-Specific Checks
- [ ] Business logic vulnerabilities
- [ ] Race condition protection
- [ ] Time-based attacks prevention
- [ ] CSRF protection implemented
- [ ] Clickjacking protection
- [ ] Directory traversal prevention
- [ ] Remote code execution safeguards

## Deployment & Operations
- [ ] Secure deployment practices
- [ ] Environment separation
- [ ] Secrets management
- [ ] Container security (if applicable)
- [ ] Network security
- [ ] Backup security
- [ ] Disaster recovery plans
- [ ] Security patch procedures

## Tools & Resources
Consider using:
- Static analysis security testing (SAST)
- Dynamic analysis security testing (DAST)
- Dependency vulnerability scanners
- Security linters
- Penetration testing tools
- OWASP guidelines and resources

## Secrets & Tokens
- [ ] No API keys, tokens, passwords, certificates, or credentials committed
- [ ] `.env*`, `*.pem`, `*.key`, `*.pfx`, `*credentials*` ignored via `.gitignore`
- [ ] Secrets are not logged or exposed in error messages
- [ ] Any leaked credentials have been rotated/invalidated
- [ ] Secret scanning performed (must pass) using one or more tools below

### Secret Scanning Commands
```bash
# Install (Windows)
choco install gitleaks
pipx install trufflehog

# Run scans
gitleaks detect --source . --redact --no-banner
trufflehog filesystem --only-verified .
```

### Git pre-commit hook (optional)
```bash
# .git/hooks/pre-commit
gitleaks detect --source . --redact --no-banner || exit 1
```

## Documentation
- [ ] Security architecture documented
- [ ] Threat model created
- [ ] Security procedures documented
- [ ] Incident response plan exists
- [ ] Security training materials available
