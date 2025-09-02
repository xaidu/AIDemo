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

## Test Artifacts & Examples

### Example Review Scenarios

#### Scenario 1: API Endpoint Addition
```javascript
// New API endpoint - focus on security and error handling
app.post('/api/users', (req, res) => {
  // ✓ Good: Input validation present
  if (!req.body.email || !req.body.password) {
    return res.status(400).json({ error: 'Email and password required' });
  }

  // ⚠️ Review: Check for SQL injection protection
  // ⚠️ Review: Verify password hashing
  // ⚠️ Review: Check rate limiting
});
```

#### Scenario 2: Database Migration
```sql
-- Migration example - focus on data safety
ALTER TABLE users ADD COLUMN last_login TIMESTAMP;

-- ✓ Good: Handles existing data
UPDATE users SET last_login = created_at WHERE last_login IS NULL;

-- ⚠️ Review: Check rollback strategy
-- ⚠️ Review: Verify no data loss
-- ⚠️ Review: Test on staging first
```

#### Scenario 3: Performance Optimization
```javascript
// Before: N+1 query problem
users.forEach(user => {
  user.posts = db.query('SELECT * FROM posts WHERE user_id = ?', user.id);
});

// After: Single optimized query
const userPosts = db.query(`
  SELECT u.*, p.title, p.content
  FROM users u
  LEFT JOIN posts p ON u.id = p.user_id
  WHERE u.active = true
`);

// ⚠️ Review: Verify query performance improvement
// ⚠️ Review: Check memory usage with large datasets
```

### Test Cases for Validation

#### Unit Test Coverage
- [ ] Happy path scenarios covered
- [ ] Error conditions tested
- [ ] Edge cases considered
- [ ] Integration points validated

#### Manual Testing Checklist
- [ ] Basic functionality works
- [ ] Error messages are clear
- [ ] UI/UX changes look correct
- [ ] Mobile responsiveness verified
- [ ] Cross-browser compatibility checked

## Review Comments
Keep comments:
- Constructive and specific
- Focused on important issues
- Clear about severity (critical vs. nice-to-have)
- Actionable for the author

### Comment Templates
- **Security Issue**: "⚠️ Security concern: [issue] - Please address before merging"
- **Performance Issue**: "🚀 Performance: [optimization needed] - Consider [solution]"
- **Bug Found**: "🐛 Bug: [description] - This will cause [problem]"
- **Improvement**: "💡 Suggestion: [enhancement] - Would improve [benefit]"
- **Question**: "❓ Question: [clarification needed] - Can you explain [aspect]?"

## Integration
- Run this command before `/create-pr` to gate changes.
- After this review, run `/security-audit` (including the Secrets & Tokens section).
- Block commit/PR if critical items remain unchecked.
- For secrets scanning commands and pre-commit hook, see `/security-audit`.
