# Git Version Control - picoCTF Writeup

## What is Git?

Git is a version control system that tracks changes to files over time. It records snapshots (commits) of your project, allowing you to view history, compare versions, and revert to previous states.

## Key Security Concepts for CTF Challenges

### Git Repository Structure

A Git repository stores all version history in a hidden `.git` directory. This directory contains:
- **Objects**: Actual file content and commit data (stored as blobs, trees, and commits)
- **Refs**: References to commits (branches, tags, HEAD)
- **Logs**: Reflogs showing when references changed
- **Config**: Repository configuration

### Accessing Hidden History

One of the most common CTF challenge patterns involves recovering information from Git history that may have been deleted from the current working directory:

```bash
# View all commits
git log

# View deleted files
git log --full-history -- <filename>

# Recover deleted content
git show <commit_hash>:<filename>

# View all refs and their history
git reflog
```

### Exposed Sensitive Data

Git repositories can inadvertently expose sensitive information:
- **Passwords or API keys** committed to history
- **Previous versions** of config files
- **Deleted branches** still accessible via reflog
- **Comments** in old commits revealing security details

Even if a file is removed in a later commit, the original content remains in the Git history and can be recovered.

### Common CTF Exploitation Techniques

**Checking git logs**: Flags are often hidden in commit messages or file contents from previous commits.

**Examining git diff**: Compare versions to find what changed, which may reveal secrets.

**Accessing reflogs**: The reflog tracks movement of HEAD and can reveal deleted branches or reset commits.

**Parsing Git objects**: Directly read from the `.git/objects` directory to extract data without using standard Git commands.

## Prevention in Real-World Scenarios

- Use `.gitignore` to prevent committing sensitive files
- Remove secrets from history using tools like `git-filter-branch` or `BFG Repo-Cleaner`
- Scan repositories for exposed credentials
- Use environment variables instead of hardcoded secrets

## Useful Git Commands for CTF

```bash
git log --oneline                    # Compact commit history
git show <commit>                    # Display commit details
git diff <commit1> <commit2>         # Compare two commits
git branch -a                        # List all branches
git checkout <commit>                # Switch to specific commit
git tag -l                           # List all tags
```