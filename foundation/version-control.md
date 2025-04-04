## **1. Initial Setup (First-Time Use)**

```sh
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

Set up your name and email for Git commits.

---

## **2. Cloning an Existing Repository**

```sh
git clone <repository-url>
```

Example:

```sh
git clone https://git.example.com/project.git
```

This downloads the repository to your local machine.

---

## **3. Checking Current Status**

```sh
git status
```

This shows which files have changed, new files, and which branch you're on.

---

## **4. Creating & Switching Branches**

```sh
git branch <branch-name>
```

Create a new branch.

```sh
git checkout <branch-name>
```

Switch to a branch.

**Shortcut: Create & Switch to a new branch in one command**

```sh
git checkout -b <branch-name>
```

Check all branches:

```sh
git branch
```

---

## **5. Pull Latest Changes**

```sh
git pull origin <branch-name>
```

This updates your local branch with the latest changes from the remote branch.

---

## **6. Adding & Committing Changes**

```sh
git add <file-name>         # Add a specific file
git add .                   # Add all modified and new files
git commit -m "Your message here"
```

This saves your changes locally.

---

## **7. Pushing Changes to Remote Repository**

```sh
git push origin <branch-name>
```

This uploads your local changes to the remote branch.

---

## **8. Merging Branches**

Switch to the main branch before merging:

```sh
git checkout main
git pull origin main
git merge <branch-name>
```

This merges `<branch-name>` into `main`.

If there are conflicts, manually fix them, then:

```sh
git add .
git commit -m "Resolved merge conflicts"
```

---

## **9. Deleting Branches**

### Locally:

```sh
git branch -d <branch-name>
```

For force deletion (if the branch is not merged):

```sh
git branch -D <branch-name>
```

### Remotely:

```sh
git push origin --delete <branch-name>
```

---

## **10. Resetting & Reverting Changes**

Undo changes in a specific file:

```sh
git checkout -- <file-name>
```

Undo all uncommitted changes:

```sh
git reset --hard
```

Undo last commit but keep changes:

```sh
git reset --soft HEAD~1
```

Undo last commit and remove changes:

```sh
git reset --hard HEAD~1
```

---

## **11. Checking Commit History**

```sh
git log --oneline --graph --all
```

---

## **12. Stashing Temporary Changes**

If you need to switch branches but have uncommitted changes:

```sh
git stash
```

Apply stashed changes later:

```sh
git stash pop
```

---

## **13. Rebase Instead of Merge (Optional)**

If you want a clean commit history:

```sh
git rebase main
```

---

### **Basic Git Flow You Should Follow**

1. **Checkout Main & Pull Latest**
   ```sh
   git checkout main
   git pull origin main
   ```
2. **Create a New Branch**
   ```sh
   git checkout -b feature-branch
   ```
3. **Work on Your Changes**
   ```sh
   git add .
   git commit -m "Implemented feature XYZ"
   ```
4. **Push to Remote**
   ```sh
   git push origin feature-branch
   ```
5. **Create a Merge Request (if applicable)**
6. **Switch Back to Main & Merge**
   ```sh
   git checkout main
   git pull origin main
   git merge feature-branch
   ```
7. **Delete Branch**
   ```sh
   git branch -d feature-branch
   git push origin --delete feature-branch
   ```

This should cover everything you need for working with Git manually. Let me know if you need clarification! 🚀
