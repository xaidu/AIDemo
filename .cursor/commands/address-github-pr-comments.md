# Address GitHub PR Comments

Comprehensive workflow for addressing reviewer feedback and comments on GitHub Pull Requests with automated tracking and resolution.

## Usage
Use this command when you need to:
- Address reviewer comments on a PR
- Make requested changes based on feedback
- Update code based on review suggestions
- Respond to specific feedback points
- Track and resolve comment threads
- Maintain professional communication with reviewers

## Prerequisites
- GitHub CLI (`gh`) installed and authenticated
- Access to the PR you want to address comments for
- Local repository synced with remote

## Automated Workflow

### 1. PR Comment Analysis
```bash
# View all PR comments and threads
gh pr view <PR_NUMBER> --comments

# Get detailed comment information
gh api repos/{owner}/{repo}/pulls/{PR_NUMBER}/comments

# List unresolved comment threads
gh pr view <PR_NUMBER> --json reviewThreads
```

### 2. Comment Processing
- **Review Comments**: Read and understand each comment carefully
- **Categorize Feedback**: Bug fixes, improvements, questions, approvals
- **Prioritize Changes**: Critical issues first, then enhancements
- **Track Resolution**: Mark threads as resolved when addressed

### 3. Code Changes
- **Identify Files**: Locate files mentioned in comments
- **Make Changes**: Implement requested modifications
- **Test Changes**: Ensure changes work correctly
- **Commit Updates**: Use meaningful commit messages

### 4. Response & Resolution
```bash
# Reply to specific comments
gh pr comment <PR_NUMBER> --body "Fixed the issue as requested"

# Mark comment threads as resolved
gh api repos/{owner}/{repo}/pulls/{PR_NUMBER}/comments/{COMMENT_ID} -X PATCH -F resolved=true

# Update PR status
gh pr edit <PR_NUMBER> --body "Updated PR description with changes made"
```

## Comment Types & Handling

### 🔧 Bug Fixes
- **Pattern**: "This causes an error when..."
- **Action**: Fix the bug, test thoroughly, explain the fix
- **Response**: "Fixed the bug by [explanation]. Added test case to prevent regression."

### ✨ Feature Requests
- **Pattern**: "Can we add...", "Consider implementing..."
- **Action**: Evaluate feasibility, implement if appropriate
- **Response**: "Added [feature] as suggested. This improves [benefit]."

### ❓ Questions/Clarifications
- **Pattern**: "Why does this...", "Can you explain..."
- **Action**: Provide clear explanation or improve code clarity
- **Response**: "Updated code with better documentation/comments to clarify [explanation]."

### 🎨 Style/Convention Issues
- **Pattern**: "Follow our style guide...", "Use consistent naming..."
- **Action**: Apply consistent formatting and conventions
- **Response**: "Applied consistent [style/convention] across the codebase."

### 🚀 Performance Concerns
- **Pattern**: "This could be optimized...", "Consider more efficient approach..."
- **Action**: Optimize code while maintaining readability
- **Response**: "Optimized [functionality] by [method], reducing [metric] by [percentage]."

## Advanced Features

### Batch Comment Resolution
```bash
# Resolve multiple comment threads at once
gh pr comment <PR_NUMBER> --body "Addressed all review comments in this commit:
- Fixed bug in [file]: [description]
- Added documentation for [feature]
- Optimized [function] performance"
```

### Comment Templates
- **Bug Fix**: "✅ Fixed: [Original Issue] - [Solution Description]"
- **Enhancement**: "✨ Added: [Feature] - [Implementation Details]"
- **Documentation**: "📚 Updated: [Documentation] - [Changes Made]"
- **Performance**: "🚀 Optimized: [Component] - [Performance Improvement]"

### Automated Testing
- Run relevant tests after changes
- Update test cases if needed
- Verify no regressions introduced

## GitHub CLI Integration

### Comment Management
```bash
# View specific comment thread
gh pr view <PR_NUMBER> --comments | grep -A 5 -B 5 "COMMENT_ID"

# Reply to a specific comment
gh pr comment <PR_NUMBER> --reply-to <COMMENT_ID> --body "Response here"

# Hide outdated comments (if you have maintainer access)
gh api repos/{owner}/{repo}/pulls/{PR_NUMBER}/comments/{COMMENT_ID} -X PATCH -F outdated=true
```

### PR Status Updates
```bash
# Mark PR as ready for review after addressing comments
gh pr ready <PR_NUMBER>

# Request re-review from specific reviewers
gh pr edit <PR_NUMBER> --add-reviewer username

# Update PR title if scope changed
gh pr edit <PR_NUMBER> --title "Updated: [New Title]"
```

## Best Practices

### Communication
- **Be Professional**: Maintain respectful tone in all responses
- **Be Specific**: Reference exact lines/files when responding
- **Be Transparent**: Explain your reasoning for decisions
- **Be Responsive**: Address comments promptly

### Code Quality
- **Test Thoroughly**: Ensure changes don't break existing functionality
- **Follow Conventions**: Maintain codebase standards and patterns
- **Document Changes**: Update relevant documentation
- **Consider Impact**: Evaluate broader implications of changes

### Workflow Efficiency
- **Batch Related Changes**: Group similar fixes in single commits
- **Update PR Description**: Reflect changes made in PR description
- **Mark Resolved Threads**: Keep PR clean by resolving completed discussions
- **Request Re-review**: Ask for re-review when significant changes are made

## Error Handling

### Common Issues
1. **Permission Denied**: Ensure you have write access to the repository
2. **Comment Not Found**: Verify comment ID and PR number are correct
3. **Merge Conflicts**: Resolve conflicts before addressing comments
4. **Outdated Comments**: Some comments may reference old code versions

### Recovery Steps
- **Sync with Remote**: `git pull origin <branch>` to get latest changes
- **Rebase if Needed**: `git rebase main` to resolve conflicts
- **Verify Changes**: Test that your fixes work with the latest code
- **Update References**: Ensure all file paths and line numbers are current

## Integration with Other Commands

### Create PR Command
- Use `/create-pr` to initially create PRs
- Use this command to address feedback on those PRs

### Code Review Checklist
- Reference `/code-review-checklist` for comprehensive review criteria
- Ensure addressed comments align with review standards

### Security Audit
- Use `/security-audit` for security-related comment resolution
- Address security concerns raised in PR feedback

## Tips
- Read each comment carefully and understand the reviewer's intent
- Ask for clarification if any feedback is unclear
- Consider the broader impact of suggested changes
- Test thoroughly after making modifications
- Be responsive and professional in your replies
- Group related changes together for efficient commits
- Keep PR descriptions updated to reflect progress
- Use comment threads effectively to maintain conversation context
