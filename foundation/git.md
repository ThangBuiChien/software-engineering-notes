# 📋 Git Take Note

## 📌 Basic Stage Flow

- **Edit file ➔ Unstaged**
- `git add filename` ➔ **Staged**
- `git commit -m "message"` ➔ **Committed**

---

## 📌 Commands

| Action                                                                      | Command                              |
| :-------------------------------------------------------------------------- | :----------------------------------- |
| Stage a file                                                                | `git add filename`                   |
| Unstage a file (move from staged ➔ unstaged)                                | `git restore --staged filename`      |
| Discard unstaged changes (reset file back to last commit)                   | `git restore filename`               |
| Discard all unstaged changes in all files                                   | `git restore .`                      |
| Reset branch to match remote (⚠️ erase all local changes and commits)       | `git reset --hard origin/branchName` |
| Clean all file that not add to staging area (⚠️ delete all untracked files) | `git clean -fd`                      |
| Stash changed changes (save them temporarily)                               | `git stash`                          |
| Apply stashed changes (restore them)                                        | `git stash apply`                    |
| View stashed changes (list)                                                 | `git stash list`                     |

---

## 📌 Working with Branches

| Action                                | Command                                |
| :------------------------------------ | :------------------------------------- |
| List local branches                   | `git branch`                           |
| List remote branches                  | `git branch -r`                        |
| List all (local + remote)             | `git branch -a`                        |
| Create new branch from current branch | `git checkout -b newBranch`            |
| Switch to an existing branch          | `git switch branchName`                |
| Create and switch to remote branch    | `git switch --track origin/branchName` |
| First push with upstream tracking     | `git push -u origin branchName`        |
| Push normally after tracking is set   | `git push`                             |
| See tracking information              | `git branch -vv`                       |

---

# ⚡ Quick Tips

- `git switch branchName` → Smart switch to local or remote branch.
- `git push -u` once → then future `git push` is enough.
- `git restore --staged` only unstages, doesn’t delete changes.
- `git reset --hard` is **dangerous** → resets everything to remote version.
