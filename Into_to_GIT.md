** Git Commands Cheatsheet**

## **1. Git Basics**

### **1.1 Setup & Configuration**
- `git config --global user.name "Your Name"`  
  *Sets your username for Git commits.*
- `git config --global user.email "your_email@example.com"`  
  *Sets your email for Git commits.*
- `git config --global core.editor "code --wait"`  
  *Sets VS Code as your default Git editor.*
- `git config --list`  
  *Displays the current Git configuration.*

### **1.2 Creating & Initializing a Repository**
- `git init`  
  *Initializes a new Git repository in the current directory.*
- `git clone <repository_url>`  
  *Clones an existing remote repository to your local machine.*

### **1.3 Basic File Operations**
- `git status`  
  *Shows the status of your working directory and staged changes.*
- `git add <file>`  
  *Stages a specific file for commit.*
- `git add .`  
  *Stages all changes in the working directory for commit.*
- `git commit -m "Commit message"`  
  *Commits staged changes with a descriptive message.*
- `git commit -am "Commit message"`  
  *Stages and commits all tracked files in one step.*

## **2. Working with Branches**
- `git branch`  
  *Lists all local branches.*
- `git branch <branch_name>`  
  *Creates a new branch.*
- `git checkout <branch_name>`  
  *Switches to an existing branch.*
- `git checkout -b <branch_name>`  
  *Creates and switches to a new branch.*
- `git branch -d <branch_name>`  
  *Deletes a branch that has been merged.*
- `git branch -D <branch_name>`  
  *Forces deletion of a branch.*

## **3. Collaborating with Remote Repositories**
### **3.1 Connecting to a Remote Repository**
- `git remote add origin <repository_url>`  
  *Connects the local repository to a remote repository.*
- `git remote -v`  
  *Lists the remote connections.*

### **3.2 Fetching and Pulling Changes**
- `git fetch`  
  *Downloads changes from the remote repository but does not merge them.*
- `git pull`  
  *Fetches and merges changes from the remote repository.*
- `git pull origin main`  
  *Pulls updates from the remote `main` branch.*

### **3.3 Pushing Changes**
- `git push origin <branch_name>`  
  *Pushes your branch changes to the remote repository.*
- `git push -u origin <branch_name>`  
  *Pushes a new branch and sets it to track the remote branch.*
- `git push`  
  *Pushes committed changes to the remote repository.*

### **3.4 Merging Changes**
- `git merge <branch_name>`  
  *Merges the specified branch into the current branch.*
- `git rebase <branch_name>`  
  *Reapplies commits from the current branch on top of another branch.*

### **3.5 Handling Merge Conflicts**
- Open the conflicting file(s) and manually resolve conflicts.
- After resolving, use:
  - `git add <file>`  
    *Stages the resolved file.*
  - `git commit -m "Resolved merge conflict"`  
    *Commits the resolved changes.*

## **4. Undoing Changes**
- `git reset HEAD <file>`  
  *Unstages a file but keeps changes.*
- `git checkout -- <file>`  
  *Discards changes in a file.*
- `git revert <commit_hash>`  
  *Reverts a commit by creating a new commit that undoes changes.*
- `git reset --soft <commit_hash>`  
  *Resets to a previous commit but keeps changes staged.*
- `git reset --hard <commit_hash>`  
  *Resets to a previous commit and discards all changes.*

## **5. Advanced Git Commands**
### **5.1 Stashing Changes**
- `git stash`  
  *Temporarily saves changes without committing.*
- `git stash list`  
  *Shows stashed changes.*
- `git stash apply`  
  *Applies the latest stash without deleting it.*
- `git stash drop`  
  *Removes the latest stash.*
- `git stash pop`  
  *Applies the latest stash and removes it from the stash list.*

### **5.2 Viewing History**
- `git log`  
  *Displays commit history.*
- `git log --oneline --graph`  
  *Shows a compact graphical representation of commit history.*
- `git diff`  
  *Shows differences between working directory and staged changes.*
- `git blame <file>`  
  *Shows who modified each line in a file and when.*

## **6. GitHub Collaboration Workflow**
### **6.1 Forking & Cloning a Repository**
- Fork the repository on GitHub.
- `git clone <forked_repository_url>`  
  *Clones the forked repository.*
- `git remote add upstream <original_repository_url>`  
  *Adds the original repository as an upstream remote.*

### **6.2 Keeping Your Fork Updated**
- `git fetch upstream`  
  *Fetches changes from the original repository.*
- `git merge upstream/main`  
  *Merges changes from the original repository into your local branch.*

### **6.3 Contributing via Pull Requests**
- Create a new branch: `git checkout -b feature-branch`
- Make changes and commit them.
- Push the branch: `git push origin feature-branch`
- Open a Pull Request on GitHub.

## **7. Git Ignore & Best Practices**
- `.gitignore` file prevents certain files from being tracked. Example:
  ```
  node_modules/
  .env
  *.log
  ````
- Keep commits small and meaningful.
- Write clear commit messages.
- Regularly pull updates from the main branch.
- Review code before merging.

This cheatsheet covers essential Git commands from setup to collaboration. By mastering these, you can efficiently manage your codebase and work seamlessly with teams!

