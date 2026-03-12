# Git + GitHub Workshop — Hands-On Practice

Welcome to the interactive portion of the workshop! Follow the steps below at your own pace. Don't worry if something goes wrong — that's what git is for.

---

## What You'll Do

1. Fork this repo and make your first commit
2. Open a Pull Request
3. Sync your fork with the original repo
4. Create a merge conflict (on purpose!) and resolve it

---

## Part 1: Fork, Commit, and Pull Request

### 🖥️ GUI (GitHub Desktop / VS Code / GitKraken)

> **Step 1 — Fork the repo**
> 1. On this repo's GitHub page, click the **Fork** button (top right)
> 2. Choose your personal account as the destination
> 3. GitHub will create a copy of this repo under your username

> **Step 2 — Clone your fork locally**
> 1. On your forked repo page, click the green **Code** button and copy the URL
> 2. In **GitHub Desktop**: File → Clone Repository → paste the URL
> 3. Choose a local folder and click **Clone**

> **Step 3 — Create your file**
> 1. Open the cloned folder on your computer
> 2. Create a new file named exactly `{github_username}.txt` (replace `{github_username}` with your actual GitHub username — e.g. `octocat.txt`)
> 3. Inside the file, type:
>    ```
>    Hello, Git!
>    ```
> 4. Save the file

> **Step 4 — Commit the file**
> 1. In **GitHub Desktop**: your new file will appear in the **Changes** panel on the left
> 2. At the bottom left, type a short commit message (e.g. `Add octocat.txt`)
> 3. Click **Commit to main**

> **Step 5 — Push to GitHub**
> 1. Click **Push origin** (top bar) to send your commit up to your fork on GitHub

> **Step 6 — Open a Pull Request**
> 1. Go to your fork on GitHub (github.com/your-username/git_workshop)
> 2. You should see a banner: **"This branch is 1 commit ahead"** — click **Contribute** → **Open pull request**
> 3. Make sure the base repo is the **original** repo (the workshop one), not your fork
> 4. Give your PR a title and click **Create pull request**
> 5. 🎉 You've opened your first PR!

---

### ⌨️ CLI (Terminal / Command Prompt / Git Bash)

> **Step 1 — Fork the repo**
> 1. On this repo's GitHub page, click the **Fork** button (top right)
> 2. Choose your personal account as the destination

> **Step 2 — Clone your fork locally**
> ```bash
> git clone https://github.com/{github_username}/git_workshop.git
> cd git_workshop
> ```

> **Step 3 — Create your file**
> ```bash
> # Replace {github_username} with your actual GitHub username
> echo "Hello, Git!" > {github_username}.txt
> ```
> Or create and edit the file manually in any text editor — just make sure it's named `{github_username}.txt` and contains `Hello, Git!`

> **Step 4 — Stage and commit the file**
> ```bash
> git add {github_username}.txt
> git commit -m "Add {github_username}.txt"
> ```

> **Step 5 — Push to GitHub**
> ```bash
> git push origin main
> ```

> **Step 6 — Open a Pull Request**
> 1. Go to your fork on GitHub (github.com/{github_username}/git_workshop)
> 2. Click **Contribute** → **Open pull request**
> 3. Make sure the base repo is the **original** workshop repo
> 4. Give your PR a title and click **Create pull request**

---

## Part 2: Syncing Your Fork

Once a few PRs have been merged into the original repo, your fork will be **out of date**. Here's how to sync it back up.

### 🖥️ GUI

> 1. On your fork's GitHub page, look for the **"This branch is X commits behind"** message
> 2. Click **Sync fork** → **Update branch**
> 3. In **GitHub Desktop**, click **Fetch origin**, then **Pull origin** to bring those changes down to your local machine

---

### ⌨️ CLI

> **Add the original repo as a remote called `upstream`** (you only need to do this once):
> ```bash
> git remote add upstream https://github.com/owhite7128/git_workshop.git
> ```
>
> **Fetch and merge the latest changes from upstream:**
> ```bash
> git fetch upstream
> git merge upstream/main
> git push origin main
> ```
> Your fork is now up to date with everyone else's changes.

---

## Part 3: Branches and Merge Conflicts

Time to break something — intentionally. This is how you learn to fix it.

### Overview of what you're doing

You're going to create two different changes to the **same line** of your `.txt` file — one on `main`, one on a new branch — and then try to merge them together. Git won't know which to keep, so it'll ask you to decide. That's a **merge conflict**.

---

### 🖥️ GUI

> **Step 1 — Create a branch (don't switch to it yet)**
> 1. In **GitHub Desktop**: Branch → New Branch → name it `conflict-branch` → click **Create Branch**
> 2. When asked, choose **"Leave my changes on main"** (or similar) — you want to stay on `main` for now
> 3. Confirm you're still on `main` — check the branch name shown in the top bar

> **Step 2 — Edit your file on main**
> 1. Open `{github_username}.txt` in a text editor
> 2. Add a new line with something coy — for example:
>    ```
>    Hello, Git!
>    I heard you like commits.
>    ```
> 3. Save the file
> 4. In GitHub Desktop: commit this change with a message like `A coy message on main`
> 5. Push to origin

> **Step 3 — Switch to your branch and make a conflicting change**
> 1. In GitHub Desktop: click the branch dropdown and switch to `conflict-branch`
> 2. Open `{github_username}.txt` again — notice your coy message isn't there (you're on a different branch!)
> 3. Add a new line that says:
>    ```
>    Hello, Git!
>    Merge Conflict
>    ```
> 4. Save, commit with a message like `Conflicting change on branch`, and push

> **Step 4 — Merge the branch into main and resolve the conflict**
> 1. Switch back to `main` in the branch dropdown
> 2. In GitHub Desktop: Branch → Merge into Current Branch → select `conflict-branch` → click **Merge**
> 3. GitHub Desktop will tell you there's a conflict. Click **Open in editor** (or open the file manually)
> 4. Your file will look something like this:
>    ```
>    Hello, Git!
>    <<<<<<< HEAD
>    I heard you like commits.
>    =======
>    Merge Conflict
>    >>>>>>> conflict-branch
>    ```
> 5. Edit the file to keep what you want (you can keep one, both, or rewrite entirely). Remove the `<<<<<<<`, `=======`, and `>>>>>>>` lines — those are git's markers, not content
> 6. Save the file
> 7. In GitHub Desktop: the file should now show as resolved — commit the merge

---

### ⌨️ CLI

> **Step 1 — Create a branch without switching to it**
> ```bash
> git branch conflict-branch
> ```
> You're still on `main`. Confirm with:
> ```bash
> git branch
> # The * shows your current branch
> ```

> **Step 2 — Edit your file on main**
> Open `{github_username}.txt` and add a new line with something coy:
> ```
> Hello, Git!
> I heard you like commits.
> ```
> Then commit:
> ```bash
> git add {github_username}.txt
> git commit -m "A coy message on main"
> ```

> **Step 3 — Switch to the branch and make a conflicting change**
> ```bash
> git switch conflict-branch
> ```
> Open `{github_username}.txt` — your coy line isn't here. Add this instead:
> ```
> Hello, Git!
> Merge Conflict
> ```
> Commit it:
> ```bash
> git add {github_username}.txt
> git commit -m "Conflicting change on branch"
> ```

> **Step 4 — Switch back to main and merge**
> ```bash
> git switch main
> git merge conflict-branch
> ```
> Git will tell you there's a conflict:
> ```
> CONFLICT (content): Merge conflict in {github_username}.txt
> Automatic merge failed; fix conflicts and then commit the result.
> ```

> **Step 5 — Open the file and resolve it**
> Your file will look like this:
> ```
> Hello, Git!
> <<<<<<< HEAD
> I heard you like commits.
> =======
> Merge Conflict
> >>>>>>> conflict-branch
> ```
> Edit it to keep what you want, and **delete all three marker lines** (`<<<<<<<`, `=======`, `>>>>>>>`). Then:
> ```bash
> git add {github_username}.txt
> git commit -m "Resolve merge conflict"
> ```
> 🎉 You resolved your first merge conflict.

---

## Reference: Commands Used Today

| What you did | CLI command |
|---|---|
| Clone a repo | `git clone <url>` |
| Check current branch | `git branch` |
| Stage a file | `git add <filename>` |
| Commit staged changes | `git commit -m "message"` |
| Push to GitHub | `git push origin main` |
| Create a branch | `git branch <name>` |
| Switch branches | `git switch <name>` |
| Merge a branch | `git merge <name>` |
| Add upstream remote | `git remote add upstream <url>` |
| Fetch from upstream | `git fetch upstream` |

---

*Made with ❤️ for the Git + GitHub workshop.*
