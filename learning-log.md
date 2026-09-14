# Git & GitHub — Learning Log

## 1. Version Control System (VCS)

A Version Control System tracks changes made to files over time. It allows developers to maintain different versions of a project, collaborate with others, and recover previous versions when necessary.

Git is a distributed version control system, while GitHub is a platform used to host Git repositories and collaborate on them.

---

## 2. Git Basic Configuration

Git identity was configured using:

```bash
git config --global user.name "Kamal Raj Giri"
git config --global user.email "girikamal2087@gmail.com"
```

Configuration can be checked using:

```bash
git config --global user.name
git config --global user.email
```

---

## 3. Repository Initialization

A Git repository can be initialized using:

```bash
git init
```

This creates the `.git` directory, which contains the information Git needs to track the project.

---

## 4. Basic Git Workflow

The basic Git workflow is:

```text
Working Directory
       ↓
   git add
       ↓
Staging Area
       ↓
  git commit
       ↓
 Local Repository
       ↓
   git push
       ↓
 Remote Repository
```

Commands practiced:

```bash
git status
git add .
git commit -m "message"
git log --oneline
```

`git commit` stores changes locally, while `git push` sends committed changes to the remote repository.

---

## 5. `.gitignore`

The `.gitignore` file specifies files and directories that Git should not track.

Example:

```text
abs
```

After adding `abs` to `.gitignore`, Git stopped showing it as an untracked file.

This is useful for excluding generated files, temporary files, environment files, dependencies, and other files that should not be committed.

---

## 6. Git Branching

Branches allow developers to work on features or changes independently.

Commands practiced:

```bash
git branch feature/homepage
git switch feature/homepage
```

A branch can also be created and switched to in one command:

```bash
git switch -c feature-name
```

The project used the following practice branches:

* `main`
* `feature/homepage`
* `conflict-practice`
* `rebase-practice`

---

## 7. GitHub Remote and SSH

The project was connected to GitHub using an SSH remote.

The remote was:

```text
git@github.com:kamalrajgiri/GitGithubDemo.git
```

The remote can be checked using:

```bash
git remote -v
```

Changes were pushed using:

```bash
git push origin main
```

and:

```bash
git push -u origin feature/homepage
```

SSH allows Git operations to communicate with GitHub without repeatedly entering credentials.

---

## 8. Pull Request

A feature branch was pushed to GitHub and a Pull Request was created from:

```text
feature/homepage → main
```

A Pull Request allows changes to be reviewed before they are merged into the target branch.

---

## 9. Merge

A branch can be merged into another branch using:

```bash
git switch main
git merge feature-name
```

Merge preserves the existing branch histories and may create a merge commit.

A merge conflict was intentionally created by modifying the same part of `index.html` differently on two branches.

The conflict was resolved manually by editing the file, staging the resolved file, and committing the result.

---

## 10. Merge Conflict

A merge conflict occurs when Git cannot automatically determine which version of a change should be kept.

During the practice, the same heading in `index.html` was modified differently on two branches.

The conflict was resolved by:

1. Opening the conflicted file.
2. Choosing the desired content.
3. Removing the conflict markers.
4. Staging the resolved file.
5. Creating the merge commit.

---

## 11. Merge vs Rebase

### Merge

Merge combines branch histories.

```text
A ── B ── C ── M
     \       /
      D ────
```

It preserves the branching structure and can create a merge commit.

### Rebase

Rebase replays commits on top of another branch.

```text
A ── B ── C ── D
             ↑
        rebased commit
```

During practice, the original commit:

```text
032af17 Add rebase practice content
```

was replayed during the rebase and became:

```text
157a8c5 Add rebase practice content
```

This demonstrated that rebase rewrites commit history and can therefore produce a new commit hash.

### Key difference

```text
Merge  → preserves history
Rebase → rewrites/replays history for a linear structure
```

Rebase should be used carefully on shared branches because it rewrites commit history.

---

## 12. Git Reset

Three reset modes were practiced.

### Soft reset

```bash
git reset --soft HEAD~1
```

Moves `HEAD` backward while keeping the changes staged.

### Mixed reset

```bash
git reset --mixed HEAD
```

Moves/reset the staging state while keeping working-directory changes.

Mixed reset is the default reset mode.

### Hard reset

```bash
git reset --hard HEAD
```

Resets the staging area and tracked working-directory changes to the selected commit.

Hard reset should be used carefully because uncommitted tracked changes can be discarded.

---

## 13. Git Stash

`git stash` temporarily stores uncommitted work so that the working directory can be cleaned.

For example:

```bash
git stash -u -m "Practice stash"
```

The `-u` option also includes untracked files.

The stash can be viewed using:

```bash
git stash list
```

and restored using:

```bash
git stash pop
```

During practice, untracked files were successfully stashed and restored.

---

## 14. Git Reflog

`git reflog` records movements of references such as `HEAD`.

Command practiced:

```bash
git reflog
```

Reflog can be useful for recovering commits after operations such as reset or rebase.

During practice, a previously created rebased commit was located and restored using its commit hash.

---

## 15. Git Fetch

```bash
git fetch origin
```

`git fetch` downloads updated information from the remote repository but does not integrate those changes into the current branch.

It updates remote-tracking references such as:

```text
origin/main
```

---

## 16. Git Pull

```bash
git pull origin main
```

`git pull` generally performs:

```text
git fetch
+
integration
```

The integration may involve a merge or rebase depending on configuration.

During practice, `git pull` caused a merge conflict because the local and remote histories had diverged.

The merge was safely cancelled using:

```bash
git merge --abort
```

---

## 17. Local and Remote Branch Divergence

The following command was used to inspect differences:

```bash
git log --oneline --left-right main...origin/main
```

The `<` symbol represented commits existing only on the local `main`, while `>` represented commits existing only on `origin/main`.

This demonstrated that local and remote branches can independently develop different histories.

---

## 18. Useful Git Commands

### Repository status

```bash
git status
```

### View history

```bash
git log --oneline
git log --oneline --graph --decorate --all
```

### View branches

```bash
git branch
git branch -vv
```

### View remote

```bash
git remote -v
```

### Fetch remote changes

```bash
git fetch origin
```

### Push changes

```bash
git push origin main
```

### Merge

```bash
git merge branch-name
```

### Rebase

```bash
git rebase main
```

### Stash

```bash
git stash
git stash list
git stash pop
```

### Reflog

```bash
git reflog
```

---

## 19. Key Learnings

* Git tracks changes locally and GitHub provides remote hosting and collaboration features.
* The staging area provides an intermediate step between editing and committing.
* `.gitignore` prevents unwanted files from being tracked.
* Branches allow independent development.
* Pull Requests provide a review and collaboration workflow.
* Merge preserves branch history and can create a merge commit.
* Rebase creates a more linear history by replaying commits and changes commit hashes.
* Reset moves branch references and has different effects depending on the mode.
* Stash temporarily stores unfinished work.
* Reflog can help recover previous `HEAD` states.
* Fetch downloads remote information without integrating it.
* Pull fetches and then integrates remote changes.
* Local and remote branches can diverge and should be inspected before deciding whether to merge, rebase, or otherwise synchronize them.

## 20. Commands Practiced

```bash
git status
git add
git commit
git log
git branch
git switch
git push
git fetch
git pull
git merge
git merge --abort
git rebase
git reset --soft
git reset --mixed
git reset --hard
git stash
git stash list
git stash pop
git reflog
git remote -v
git branch -vv
```
