# Create Pull Request

Command to interactively create a well-structured PR: branch, review changes, commit, push, and open a PR with a clear template.

## Usage
Use this when you have local changes and want to open a PR.

## Inputs To Collect
- Jira ticket (optional), e.g. `ABC-123`
- Brief description, e.g. `add user profile card`
- Files to include in the commit (all or selected)
- Confirmation to commit and push

## Branch Rules
- If on `main` or `master`, create a new branch.
- Branch format (preferred): `[Jira-Ticket]/brief-description` (kebab-case description).
  - Examples: `ABC-123/add-user-profile-card`, `FEAT/add-telemetry`
  - Fallback if no ticket: `feat/brief-description`

## Interactive Flow
1. Detect current git state:
   - Show current branch, remotes, and `git status -s`.
   - If on `main/master`, create a feature branch per Branch Rules.
2. Review changes:
   - Show `git diff --name-only` and a short summary diff for each file.
   - Ask which files to include (or `all`).
3. Confirm commit:
   - Build commit title: `[Jira-Ticket] brief description` (omit ticket if none).
   - Ask for confirmation to commit with the selected files.
4. Commit and push:
   - Stage chosen files.
   - Commit with the constructed message.
   - Push with upstream: `git push -u origin <branch>`.
5. Create PR:
   - Title format: `[type or Jira-Ticket]: brief description`
     - If Jira present: `[ABC-123]: add user profile card`
     - Else: `[feat]: add user profile card` (choose `fix|feat|docs|chore|refactor|test` as appropriate)
   - Body uses the PR Description Template below.
   - If GitHub CLI (`gh`) available, run:
     - `gh pr create --base main --head <branch> --title "<title>" --body "<body>"`
   - Otherwise, open the repo compare URL for manual PR creation:
     - `https://github.com/<owner>/<repo>/compare/main...<branch>?expand=1`
6. Post-creation:
   - Add reviewers, labels, and link related issues.
   - Be responsive to feedback and update as needed.

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

## Pre-flight Checks (Before Creating PR)
1. Ensure your branch is up to date with main/master
2. Verify the build passes locally
3. Review your own changes first
4. Write meaningful commit messages
5. Squash commits if necessary

## Prompts The Assistant Should Ask
- Jira ticket (optional):
- Brief description (required):
- Files to include (comma-separated or `all`):
- Commit now? (y/N):
- Push to remote and open PR? (y/N):

## Notes
- Include changed items in the commit and PR description.
- Confirm with the user before committing and pushing.
- Clearly document any breaking changes in the PR.
