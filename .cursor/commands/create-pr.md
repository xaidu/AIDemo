# Create Pull Request

Command to automatically create a well-structured PR with branch creation, review, commit, push, and GitHub PR creation.

## Usage
Use this when you have local changes and want to open a PR. This command will automatically:
- Create feature branches
- Stage and commit changes
- Push to remote
- Create PR with GitHub CLI (or provide manual URL if CLI unavailable)

## Prerequisites
- GitHub CLI (`gh`) installed and authenticated
- Repository has a remote origin configured
- User has necessary permissions to create PRs

## Inputs To Collect
- Jira ticket (optional), e.g. `ABC-123`
- Brief description (required), e.g. `add user profile card`
- Files to include (default: `all`)
- Draft PR? (y/N)
- Add reviewers (optional, comma-separated)
- Add labels (optional, comma-separated)

## Branch Rules
- If on `main` or `master`, create a new branch.
- Branch format (preferred): `[Jira-Ticket]/brief-description` (kebab-case description).
  - Examples: `ABC-123/add-user-profile-card`, `FEAT/add-telemetry`
  - Fallback if no ticket: `feat/brief-description`

## Automated Flow
1. **Environment Check**:
   - Verify GitHub CLI installation and authentication
   - Detect repository information (owner, name, default branch)
   - Check current git status and branch

2. **Branch Management**:
   - If on `main/master`, create feature branch automatically
   - Branch name: `[Jira-Ticket]/brief-description` or `feat/brief-description`

3. **Change Review**:
   - Show summary of changed files and modifications
   - Automatically stage all changes (or allow file selection)

4. **Commit & Push**:
   - Create commit with standardized message: `[Jira-Ticket] brief description`
   - Push to remote with upstream tracking

5. **PR Creation**:
   - **Automatic Mode (Preferred)**:
     - Use `gh pr create` with rich description
     - Add reviewers, labels, and assignees automatically
     - Set as draft if requested
   - **Fallback Mode**:
     - Generate GitHub compare URL for manual creation
     - Provide pre-filled PR template

6. **Post-Creation**:
   - Display PR link and details
   - Suggest next steps for review and merging

## PR Description Template

### Summary
Brief description of what this PR accomplishes.

### Changes Made
- List the main changes
- Mention new features or bug fixes
- Note any breaking changes

### Testing
- Describe how you tested the changes
- Include manual testing steps if applicable
- Note any automated tests added or modified

### Additional Notes
Any additional context, concerns, or information reviewers should know.

## GitHub CLI Commands

### Setup & Authentication
```bash
# Install GitHub CLI (if not already installed)
winget install --id GitHub.cli
# OR
choco install gh

# Authenticate with GitHub
gh auth login

# Check authentication status
gh auth status
```

### Repository Detection
```bash
# Get repository information
gh repo view --json owner,name,defaultBranchRef

# List available branches
gh api repos/{owner}/{repo}/branches | jq -r '.[].name'
```

### PR Creation Commands
```bash
# Create PR with basic info
gh pr create --base main --head feature-branch --title "Title" --body "Description"

# Create draft PR
gh pr create --draft --base main --head feature-branch --title "Title"

# Add reviewers and labels
gh pr edit 1 --add-reviewer username1,username2 --add-label bug,enhancement

# Add assignees
gh pr edit 1 --add-assignee username
```

## Error Handling

### Common Issues & Solutions
1. **GitHub CLI not installed**:
   - Install via: `winget install --id GitHub.cli`
   - Alternative: Download from https://cli.github.com/

2. **Authentication failed**:
   - Run: `gh auth login`
   - Choose authentication method (browser/oauth recommended)

3. **No remote repository**:
   - Add remote: `git remote add origin https://github.com/owner/repo.git`
   - Verify: `git remote -v`

4. **Branch already exists**:
   - Delete local: `git branch -D branch-name`
   - Delete remote: `git push origin --delete branch-name`

5. **Permission denied**:
   - Check repository permissions on GitHub
   - Verify token scopes include 'repo' and 'workflow'

## Pre-flight Checks (Before Creating PR)
1. ✅ Ensure your branch is up to date with main/master
2. ✅ Verify the build passes locally
3. ✅ Review your own changes first
4. ✅ Write meaningful commit messages
5. ✅ Squash commits if necessary
6. ✅ Confirm GitHub CLI is authenticated
7. ✅ Verify repository remote is configured

## Interactive Prompts
- Jira ticket (optional):
- Brief description (required):
- Files to include (default: `all`):
- Draft PR? (y/N):
- Add reviewers (optional, comma-separated):
- Add labels (optional, comma-separated):
- Commit and push now? (y/N):

## Advanced Features

### Branch Protection
- Automatically checks if branch protection rules allow direct pushes
- Suggests creating PR even if branch protection is enabled

### Commit Message Standards
- Enforces conventional commit format when possible
- Supports Jira ticket integration in commit messages

### PR Templates
- Auto-detects and uses repository PR templates
- Falls back to built-in template if none exist

### Notifications
- Can notify team members when PR is created
- Supports Slack/webhook integrations (future enhancement)

## Notes
- Include changed items in the commit and PR description.
- Confirm with the user before committing and pushing.
- Clearly document any breaking changes in the PR.
- PR creation is fully automated when GitHub CLI is properly configured.
- Fallback to manual URL generation if CLI is unavailable.
