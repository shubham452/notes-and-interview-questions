Here’s a comprehensive list of **Git commands** commonly used in **software development**, categorized by use case:

---

## 🔹 **1. Setup and Configuration**

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global core.editor "code --wait"         # Set VS Code as editor
git config --list                                      # View all config
```

---

## 🔹 **2. Repository Initialization**

```bash
git init                                              # Initialize new local repo
git clone <repo-url>                                  # Clone remote repo
```

---

## 🔹 **3. Basic Snapshotting**

```bash
git status                                            # Check status
git add <file>                                        # Stage a file
git add .                                             # Stage all files
git reset <file>                                      # Unstage file
git commit -m "your message"                          # Commit staged changes
git commit -am "msg"                                  # Add + commit tracked files
```

---

## 🔹 **4. Branching**

```bash
git branch                                            # List branches
git branch <branch-name>                              # Create new branch
git checkout <branch-name>                            # Switch branch
git checkout -b <branch-name>                         # Create + switch
git branch -d <branch-name>                           # Delete branch (merged)
git branch -D <branch-name>                           # Force delete
```

---

## 🔹 **5. Merging and Rebasing**

```bash
git merge <branch-name>                               # Merge into current
git rebase <branch-name>                              # Rebase onto
git rebase -i HEAD~3                                  # Interactive rebase last 3 commits
git merge --abort                                     # Abort merge
git rebase --abort                                    # Abort rebase
```

---

## 🔹 **6. Remote Repositories**

```bash
git remote -v                                         # View remotes
git remote add origin <url>                           # Add remote
git push -u origin <branch-name>                      # Push and track
git push                                              # Push current branch
git fetch                                             # Fetch latest refs
git pull                                              # Pull + merge
git pull --rebase                                     # Pull + rebase
```

---

## 🔹 **7. Stashing Work**

```bash
git stash                                             # Stash changes
git stash list                                        # List stashes
git stash apply                                       # Apply latest stash
git stash apply stash@{1}                             # Apply specific stash
git stash pop                                         # Apply and remove
git stash drop stash@{0}                              # Drop specific stash
```

---

## 🔹 **8. Undoing Changes**

```bash
git checkout -- <file>                                # Discard local changes
git restore <file>                                    # Same as above (new)
git reset HEAD~1                                      # Undo last commit (keep changes)
git revert <commit-id>                                # Create reverse commit
```

---

## 🔹 **9. Logs and Diffs**

```bash
git log                                               # Commit history
git log --oneline                                     # One-line log
git log --graph --oneline --all                       # Graph view
git diff                                              # Show unstaged changes
git diff --staged                                     # Show staged changes
```

---

## 🔹 **10. Tags and Releases**

```bash
git tag                                               # List tags
git tag v1.0                                          # Create tag
git tag -a v1.0 -m "message"                          # Annotated tag
git push origin v1.0                                  # Push tag
git push origin --tags                                # Push all tags
```

---

## 🔹 **11. Clean Up**

```bash
git clean -n                                          # Show what would be deleted
git clean -f                                          # Delete untracked files
git gc                                                # Cleanup unnecessary files
```

---

## 🔹 **12. Advanced Tools**

```bash
git cherry-pick <commit-id>                           # Apply a commit from another branch
git blame <file>                                      # Who changed what and when
git bisect start                                      # Begin binary search
git bisect bad
git bisect good <commit-id>                           # Locate breaking commit
git submodule add <url> path/                         # Add submodule
```

---

## 🔹 **13. GitHub / GitLab Integration (Optional)**

```bash
gh repo clone owner/repo-name                         # GitHub CLI clone
gh pr create                                          # Create pull request
gh pr checkout <id>                                   # Checkout PR branch
```

---

## ✅ Most Frequently Used in Daily Development

```bash
git status
git add .
git commit -m "..."
git pull
git push
git checkout -b feature/xyz
git merge dev
```

---

Would you like me to turn this into a printable cheat sheet or categorized markdown for docs use?
