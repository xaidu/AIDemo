# Light Review of Existing Diffs

Quick review process for existing code changes and diffs.

## Purpose
Perform a focused, efficient review of code changes without doing a deep dive into every detail.

## Quick Review Checklist

### High-Level Review
- [ ] Changes align with the stated purpose
- [ ] No obvious red flags or major issues
- [ ] File structure changes make sense
- [ ] Overall approach seems reasonable

### Code Quality Spot Checks
- [ ] Check a few functions for clarity and logic
- [ ] Look for obvious bugs or typos
- [ ] Verify error handling in key areas
- [ ] Check for consistent coding style

### Security & Performance
- [ ] No obvious security vulnerabilities
- [ ] No major performance anti-patterns
- [ ] Sensitive data handled appropriately
- [ ] Database queries look efficient

### Testing & Documentation
- [ ] Tests exist for main functionality
- [ ] Critical paths are covered
- [ ] Documentation updated if needed
- [ ] Breaking changes documented

## Focus Areas for Light Review
1. **New public APIs** - These need careful review
2. **Security-related changes** - Always review thoroughly
3. **Database migrations** - Check for data safety
4. **Error handling** - Ensure proper error management
5. **Performance-critical code** - Review for efficiency

## What to Skip in Light Review
- Detailed style nitpicks
- Minor variable naming issues
- Non-critical refactoring details
- Extensive testing of edge cases

## When to Escalate
- Security concerns found
- Major architectural issues
- Breaking changes not documented
- Complex logic that needs deeper review
- Potential performance problems

## Review Comments
Keep comments:
- Constructive and specific
- Focused on important issues
- Clear about severity (critical vs. nice-to-have)
- Actionable for the author
