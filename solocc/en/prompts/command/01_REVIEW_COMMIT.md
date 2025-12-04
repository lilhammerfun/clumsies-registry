# Review Commit

## Description

Check current git changes, analyze modifications, and generate commit message suggestions that comply with project standards.

## Execution Steps

1. **View modification status**
   - Run `git status` to view list of modified files
   - Identify modules and scope affected by changes

2. **View specific changes**
   - Run `git diff` to view unstaged changes
   - Run `git diff --cached` to view staged changes
   - Analyze the nature of changes (new feature, fix, refactor, etc.)

3. **Generate commit message**
   - Analyze change type per `conduct/GIT_COMMIT.md` standards
   - Determine commit type: feat/fix/refactor/docs/chore, etc.
   - Determine scope of impact
   - Write concise and accurate description (subject)
   - If needed, write detailed explanation (body)

4. **Output suggestions**
   - Present suggested commit message to user
   - Explain reasoning for choosing that type and description
   - Wait for user confirmation or modification

## Notes

- **Never auto-commit**: Only generate suggestions, never execute `git add` or `git commit`
- **Follow standards**: Strictly follow `conduct/GIT_COMMIT.md` format requirements
- **Use English**: Commit messages must be in English
- **Accuracy first**: If changes are complex, suggest user split into multiple commits
- **Check sensitive info**: If .env, credentials, or other sensitive files are found, warn user not to commit
