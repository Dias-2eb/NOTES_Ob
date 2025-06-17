Basic comands:
Git log –shows all commits 
Cd –moves to working directory 
Pwd –shows current directory 
Git clone ssh – clones code repository 
Ls –shows content 
Gite remote-v – to check the origin of repository 
git status- check the status 
Git add file_name – adds to stationaryy phase 
Git commit –m "__" - commits 
Git push – pushes 
Git pull – pulls the changes
![[Pasted image 20250410113811.png]]

![[Pasted image 20250410112219.png]] 
GIT Undoing the changes
![[Pasted image 20250410112411.png]]
GIT ERROR: remote `main` branch has changes that your local `main` branch doesn’t have.
![[Pasted image 20250410114633.png]]
DIFFERENCES
![[Pasted image 20250410123540.png]]
## **1. `git reset` (Undo Commits and Changes)**

👉 Used to move the branch pointer back to a previous commit and optionally remove changes.

### **Modes of `git reset`:**

1. **Soft Reset (`git reset --soft <commit>`)**
    
    - Moves the branch pointer to `<commit>` but **keeps changes staged**.
        
    - Useful when you want to redo the last commit but keep your changes ready to commit again.
        
    - Example: git reset --soft HEAD~1  # Undo last commit, keep changes staged`
        
2. **Mixed Reset (Default, `git reset --mixed <commit>`)**
    
    - Moves the branch pointer to `<commit>`, **unstages changes**, but keeps them in the working directory.
        
    - Example:
        
        
        
        `git reset HEAD~1  # Undo last commit and unstage changes`
        
3. **Hard Reset (`git reset --hard <commit>`)**
    
    - Moves the branch pointer to `<commit>` and **deletes all changes** (both staged and unstaged).
        
    - ⚠ **Warning:** This is destructive and removes changes permanently!
        
    - Example:
        
        
        
        `git reset --hard HEAD~1  # Completely remove last commit`
        

---

## **2. `git revert` (Create a New Commit to Undo Changes)**

👉 Used to **reverse** a commit **without modifying commit history**.

- Creates a **new commit** that undoes the changes of a previous commit.
    
- Useful when working in a shared repository because it **does not rewrite history**.
    
- Example:
    
    
    
    `git revert HEAD  # Reverts the last commit by creating a new commit`
    
- If you want to revert a specific commit (not the latest one):
    
    
    
    `git revert <commit-hash>`
    
- If you want to **skip the commit message editor**:
    

    
    
    
    `git revert -n <commit-hash>  # Undo changes without committing immediately`
    

✅ **Best for:** Reverting changes in a shared repository safely.

---

## **3. `git commit --amend` (Modify the Last Commit)**

👉 Used to **change** the last commit without creating a new one.

- You can edit the commit message:
    
    
    
    `git commit --amend`
    
- You can add changes to the last commit:
    
    
    
    `git add <file> git commit --amend --no-edit  # Modify the last commit without changing its message`
    
- If you already pushed the commit, you need to force push:
    
    sh
    
    КопироватьРедактировать
    
    `git push --force origin main  # Be careful! This rewrites history`
    

✅ **Best for:** Fixing mistakes in the last commit before pushing.

.gitignore


![[Pasted image 20250415104616.png]]
![[Pasted image 20250415104631.png]]
![[Pasted image 20250415104642.png]]
![[Pasted image 20250415105630.png]]
![[Pasted image 20250415105652.png]]
### 🟢 **Fast-Forward Merge**

A **fast-forward** happens when there’s a **direct path** from the current branch tip to the branch being merged.

#### 📌 What happens:

- Git just **moves the pointer** forward to the new commit.
    
- No new merge commit is created.
    

#### 🧠 Think of it like:

> "Hey, your current branch hasn’t diverged at all. Just move the pointer forward."

#### ✅ Conditions:

- Your branch has **no unique commits** since the branch you’re merging in.
    

#### 📊 Example:

bash

`main:    A---B                  \ feature:          C---D`

You run:

`git checkout main git merge feature`

Because `main` has no new commits, Git just **slides `main` forward** to `D`. No merge commit is created.

---

### 🔴 **Non-Fast-Forward Merge**

A **non-fast-forward** happens when the branches have **diverged** — both have new commits.

#### 📌 What happens:

- Git **creates a new merge commit** to join the histories.
    

#### 🧠 Think of it like:

> "Hmm, both branches have moved. I’ll glue them together with a merge commit."

#### ✅ Conditions:

- Your branch has **new commits of its own** that don’t exist in the branch being merged.
    

#### 📊 Example:

bash

You run:

`git checkout main git merge feature`

Git can’t just move the pointer. So it creates a **new commit** `F`:

bash


`main:    A---B---E          \       \ feature:  C---D---F (merge commit)`

---

### 🛠 Force Push & Non-Fast-Forward Rejection

When Git tells you:

css

КопироватьРедактировать

`! [rejected]        main -> main (non-fast-forward)`

It means your local history and remote history have **diverged**, and Git refuses to overwrite the remote without you explicitly saying so (via `--force`).

---

### ✅ Summary Table

|Feature|Fast-Forward|Non-Fast-Forward|
|---|---|---|
|Pointer Movement|Simple pointer move|Creates a merge commit|
|Histories Diverged?|No|Yes|
|Keeps History Clean?|Yes|No (unless squash merge is used)|
|Use Case|Linear history|Preserving complete history|
![[Pasted image 20250415142434.png]]
![[Pasted image 20250415143217.png]]
![[Pasted image 20250416113026.png]]![[Pasted image 20250416123407.png]]
![[Pasted image 20250416125029.png]]
