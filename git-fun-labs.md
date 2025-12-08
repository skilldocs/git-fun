# Git Fundamentals
## Understanding and using Git effectively
## Session labs
## Revision 4.0 - 12/08/25
© 2025 Brent Laster & Tech Skills Transformations LLC

<br><br>
---

## Important Notes Before Starting

**Note 1 — GitHub Personal Access Token (PAT)**  

Before Lab 6, you must have a GitHub account **and a Personal Access Token**. You will have a choice of a *fine-grained* token or a *classic* token. We will use *classic*.

Below is a link with detailed instructions.

[Instructions to create token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic)

When ready, you can create a token quickly with the direct link below. Be sure the **repo** scope is enabled (clicked). You will need to supply a comment, **create the token and copy it to have for later.**

[Quick link to initialize token](https://github.com/settings/tokens/new?scopes=repo)

![Get new token](./images/git1.png?raw=true "Get new token") 

![save new token](./images/git2.png?raw=true "Save new token") 

<br><br>

**Note 2 - Arguments in Capital letters**

In the labs, arguments in CAPS indicate placeholders for names you can pick.

<br><br>

---

# Lab 1 — Creating and Exploring a Git Repository & Managing Content

## Lab Purpose
Create a new Git repository, configure your identity, add files, stage them, and commit updates.

<br><br>

## Prerequisites
- Git installed (version **2.0+**)
- Confirm version using:
  ```bash
  git --version
  ```
<br><br>

---

## Steps

### 1. Create a working directory and change into it. This will be the directory we work in unless otherwise specified.
```bash
mkdir WORKDIR
cd WORKDIR
```

<br><br>

### 2. Initialize a new Git repository in the directory by running the command below.
```bash
git init
```
This creates a `.git` directory that stores all repository metadata. You are now able to start using other Git commands in the current directory.

<br><br>

### 3. Configure your Git identity. Tell Git who you are by setting your required configuration settins with the following commands.

Note the double dashes before **global** since we are spelling out the option. Also, values only require quotes if there is a space in the value.

```bash
git config --global user.name "FIRST_NAME LAST_NAME"
git config --global user.email YOUR_EMAIL_ADDRESS
```

<br><br>

### 4. Create some content to work with. 

Note that for purposes of these initial labs, we just need files to work with - we don’t really care what’s in them. We can “cheat” and just echo something into a file
via the “>” operator. In fact, the output of any command could be used to put content into a file via the “>” operator. Of course, if you prefer, you can
certainly create files via your favorite editor instead.

```bash
echo content > FILE1
echo content > FILE2
```

<br><br>

### 5. Stage the files with the add command. 

If you prefer, you can add each file separately rather than use the ".".

```bash
git add .
```

<br><br>

### 6. Commit the files.

You can use whatever commit message (comment) you want. Note the single hyphen/dash before the short form of the option.

```bash
git commit -m "COMMIT_MSG"
```

<br><br>

### 7. Observe the commit output.

You will see the branch name (`main`), the note `root-commit`, and the short SHA-1.

<br><br>

### 8. Modify one of your files.

We can just use the “>>” to append something tothe file’s content.

```bash
echo more >> FILE1
```

<br><br>

### 9. Stage + commit the modified file using the shortcut. 

Note the combined short options *-am* for *-a* + *-m*.

```bash
git commit -am "COMMIT_MSG"
```

---

<p align="center">
<br>[END OF LAB]<br>
</p>
</br></br>



# Lab 2 — Tracking Content Through the File Status Lifecycle

## Lab Purpose
Explore how Git tracks changes across the Working Directory, Staging Area, and Local Repository.

<br><br>

## Prerequisites
- Completed **Lab 1**
- You are in the same repository directory used in Lab 1

<br><br>

---

## Steps

### 1. Check clean status.

Run the status command or the short form to see how it looks when you have no changes to be staged or committed.

```bash
git status
# or
git status -s
```

<br><br>

### 2. Create a new file and view the status.

```bash
echo content > FILE3
git status
```

Question: Is the file *tracked* or *untracked*?

Answer: It’s **untracked** - we haven’t added the initial version to Git yet.

<br><br>

### 3. Stage the file and check status.

```bash
git add FILE3
git status
```

Questions: Is the file *tracked* or *untracked*? What does *Changes to be committed* mean?

Answers: The file is now **tracked** - we’ve added the initial version to Git.
**Changes to be committed** implies files exist in the Staging Area and the
next step for them is to be committed into the Local Repository.

<br><br>

### 4. Edit the file again and check the status.

```bash
echo change > FILE3
git status
```

Questions: 

- Why do we see two?
- Where is the version that’s listed as *Changes to be committed*? (Working Directory, Staging Area, or Local Repository)
- Where is the version that’s listed as *Changes not staged for commit*? (Working Directory, Staging Area, or Local Repository)

Answers: 
- We see two because there is one version of the same file in the Working Directory and another version in the Staging Area.
- The version that’s listed as **Changes to be committed** is in the Staging Area. The phrase implies that this version’s “next step” or “next level for promotion” is to the Local Repository via a commit.
- The version that’s listed as **Changes not staged for commit** is in the Working Directory. The phrase implies that this version’s “next step” or “next level for promotion” is to the Staging Area, since it’s currently “not staged”.)

<br><br>

### 5. Do a diff between the version in the Working Directory and the version in the Staging Area.

```bash
git diff
```

<br><br>

### 6. Commit the staged version and do another status check.

```bash
git commit -m "COMMIT_MSG"
git status
```

Question: Which version did we commit – the one in the Staging Area or the one in the Working Directory? (Hint: Which one is left – shows up in the status? Note
the **Changes not staged for commit** part of the status message.)

Answer: The version in the Staging Area was the one committed. The content goes through the Staging Area and then into the Local Repository.

<br><br>

### 7. Stage the modified file you have in your Working Directory and do a status check.

```bash
git add .
git status
```

<br><br>

### 8. Edit the file again in the Working Directory and do a status check.

```bash
echo change 2 > FILE3
git status
```

Now there are three versions:
- Local Repository version (committed in step 6)
- Staging Area version (staged in step 7)
- Working Directory version (step 8)

 <br><br>

### 9. Diff the version in the Working Directory against the version in the Staging Area.

```bash
git diff
```

<br><br>

### 10. Diff the version in the Staging Area against the version in the Local Repository.

```bash
git diff --staged
# or
git diff --cached
```

<br><br>

### 11. Diff the version in the Working Directory against the version in the Local Repository (the one we committed earlier).

```bash
git diff HEAD
```

### 12. Commit using the shortcut
```bash
git commit -am "commit-message"
```

Question: Which version got committed – the one in the Working Directory or the one in the Staging Area?

Answer: Since we used the *-am* shortcut, the version from the Working Directory was staged (over the previous version in the Staging Area) and then that version was committed into the Local Repository.

<br><br>

### 13. Verify that the status shows a clean state.

```bash
git status
```

Notice the output - we’re back to a clean Working Directory - Git has the
latest versions of everything we’ve updated.

---

<p align="center">
<br>[END OF LAB]<br>
</p>
</br></br>


# Lab 3 — Working With Changes Over Time & Using Tags

## Lab Purpose
Explore commit history, logs, aliases, and tagging commits for easier reference.

<br><br>

## Prerequisites
- Completed **Lab 2**
- You are in the same repository directory used previously

<br><br>

---

## Steps

### 1. Add another change
```bash
echo new >> file1-name
git commit -am "commit-message"
```

### 2. View history
```bash
git log
```

### 3. View one-line history
```bash
git log --oneline
```

### 4. Use formatted log output
```bash
git log --pretty=format:"%h %ad|%s %d[%an]" --date=short
```

### 5. Create a helpful alias for the formatted history
```bash
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --date=short"
```

### 6. Run the alias
```bash
git hist
```

### 7. Show history for a single file
```bash
git hist file1-name
```

### 8. Identify earliest & latest commit SHAs
Run:
```bash
git hist
```
Note the SHA of:
- The earliest commit (bottom of the list)
- The latest commit (top of the list)

### 9–10. View history between two SHAs
```bash
git hist earliest-SHA1..latest-SHA1
```

### 11. View diff for a file across that range
```bash
git diff earliest-SHA1..latest-SHA1 file1-name
```

### 12. Create tags for earliest and latest commits
```bash
git tag first earliest-SHA1
git tag last latest-SHA1
```

### 13. Use tags instead of SHAs in history commands
```bash
git hist first..last
```

### 14. Show filenames that changed
```bash
git hist first..last --name-only
```

### 15. Filter by file
```bash
git hist first..last --name-only file1-name
```

---

## END OF LAB 3



# Lab 4 — Working With Branches

## Lab Purpose
Create branches, switch between them, and compare different file versions.

<br><br>

## Prerequisites
- Completed **Lab 3**
- In the same repository directory

<br><br>

---

## Steps

### 1. View existing branches
```bash
git branch
```

### 2. Interpret the branch list
You should see:
- `* main` — only one branch, and `main` is the current branch.

### 3. Update a file on `main`
```bash
echo "main version" >> file-name
git commit -am "main version"
```

### 4. Create a feature branch
```bash
git branch feature-branch-name
```

### 5. Verify branches
```bash
git branch
```
You should now see:
- `main`
- `feature-branch-name`

### 6. Switch to the feature branch
```bash
git checkout feature-branch-name
```

### 7. Verify you are on the feature branch
```bash
git branch
```
The `*` should now be next to `feature-branch-name`.

### 8. Create a new file on the feature branch
```bash
echo some-text > new-file
```

### 9. Update an existing file to indicate the feature branch
```bash
echo "feature version" >> file-name
```

### 10. Stage and commit your changes
```bash
git add .
git commit -m "feature version"
```

### 11. Switch back to `main`
```bash
git checkout main
```

### 12. Verify you're on `main`
```bash
git branch
```

### 13. Check file contents on `main`
```bash
cat *
```
Look for `main version` in the file(s). The feature-branch updates should not be present here.

---

<p align="center">
<br>[END OF LAB]<br>
</p>
</br></br>


# Lab 5 — Practice With Merging

## Lab Purpose
Practice merging branches, observing conflicts, and resolving them.

<br><br>

## Prerequisites
- Completed **Lab 4**
- In the same repository directory

<br><br>

---

## Steps

### 1. Verify clean working state
```bash
git status
```
You should see: `working tree clean`.

### 2. Create a new file on `main`
```bash
echo "some-text" > file5-name
```

### 3. Stage and commit on `main`
```bash
git add .
git commit -m "adding new file on main"
```

### 4. Create a new branch (but do not switch yet)
```bash
git branch new-branch
```

### 5. Change the file on `main`
```bash
echo "Update on main" > file5-name
```

### 6. Stage and commit the change on `main`
```bash
git add .
git commit -m "update on main"
```

### 7. Switch to `new-branch`
```bash
git checkout new-branch
```

### 8. Change the same line in the same file on `new-branch`
```bash
echo "Update on new-branch" > file5-name
```

### 9. Commit the change on `new-branch`
```bash
git commit -am "update on new-branch"
```

### 10. Switch back to `main`
```bash
git checkout main
```

### 11. Merge `new-branch` into `main`
```bash
git merge new-branch
```

### 12. Check status for conflicts
```bash
git status
```

### 13. Inspect the conflict markers
```bash
cat file5-name
```
You should see conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).

### 14. Fix the conflict
For simplicity, overwrite the file with a merged version:
```bash
echo "merged version" > file5-name
```

### 15. Stage and commit the resolved file
```bash
git commit -am "Fixed conflicts"
```

### 16. Verify the merge is complete
```bash
git status
```

### 17. Delete the merged branch
```bash
git branch -d new-branch
```

---

<p align="center">
<br>[END OF LAB]<br>
</p>
</br></br>


# Lab 6 — Using the Complete Git Workflow With a Remote Repository

## Lab Purpose
Fork a remote repository on GitHub, clone it locally, work with branches and rebasing, handle push rejections, and resolve them.

<br><br>

## Prerequisites
- GitHub account
- GitHub Personal Access Token (Classic) with **repo** scope

<br><br>

---

## Steps

### 1. Sign in to GitHub
Go to:

```text
https://github.com
```

Sign in with your GitHub account.

### 2. Navigate to the `calc3` project
Visit:

```text
https://github.com/skillrepos/calc3
```

### 3. Fork the repository
- Click **Fork** (top right).
- Uncheck **Copy the main branch only** so you also get other remote branches.
- Click **Create fork**.

Your URL should now look like:

```text
https://github.com/your-github-userid/calc3
```

### 4. Get the clone URL
- On your fork page, click the green **<> Code** button.
- Select the **Local** tab.
- Unless you already have SSH set up, choose **HTTPS**.
- Click the **copy** icon next to the HTTPS URL to copy it to your clipboard.

### 5. Clone the project locally
In your terminal:

```bash
cd ..   # if needed, to get out of the previous lab repo
git clone https://github.com/your-github-userid/calc3.git
cd calc3
```

### 6. Confirm clone contents
List files and ensure `.git` exists:

```bash
ls -la
```

### 7. Inspect remote branches
```bash
git branch -r
git branch -av
```

### 8. View remote configuration
```bash
git remote -v
```

### 9. (Optional) Open the calculator in a browser
Open `calc.html` in a browser and confirm it supports basic arithmetic operations.

### 10. Create a local branch to track the remote `features` branch
```bash
git branch features origin/features
```

### 11. Inspect history on `main` and `features`
```bash
git log --oneline          # main
git log --oneline features # features
```

### 12. Rebase `features` onto `main`
While on `main`:

```bash
git rebase features
```

This applies the commits from `features` onto your local `main` branch.

### 13. Inspect updated history
```bash
git log --oneline
```

(Optionally, open `calc.html` in a browser to see new functions such as max, min, exp, etc.)

### 14. Push updates to your fork (expect a rejection)
```bash
git push -u origin main
```

You will be prompted for:
- Username (your GitHub username)
- Personal Access Token (paste your PAT when asked for password/token)

You should see a **non-fast-forward** rejection error. This is expected.

### 15. Understand the rejection
The rebase rewrote history so your local `main` has commits that Git cannot fast-forward to on the remote. You must first bring down any remote changes and merge them.

### 16. Pull from remote with merge
```bash
git pull --no-rebase
```

Git may open an editor for the merge commit message. Save and close the editor to complete the merge.

### 17. Push again (should succeed)
```bash
git push origin main
```

Use your PAT again if prompted.

### 18. Verify on GitHub
Refresh your fork’s GitHub page and confirm:
- The history reflects your rebase and merge.
- The new features (max, exp, min) are present in `calc.html` in the repository.

---

<p align="center">
<br>[END OF LAB]<br>
</p>
</br></br>


# Appendix — Credential Helper / SSH Options

If HTTPS authentication fails (for example, due to old or incorrect stored credentials), use one of the following approaches.

## Option A — Reset Credential Helper

Reset or adjust your credential helper:

```bash
git config --global credential.helper store
```

If you prefer to disable a system-level credential helper (if permitted):

```bash
git config --unset --system credentials.helper
```

After updating this, try your `git push` again. You will be prompted for credentials, and you can paste your PAT.

## Option B — Use SSH Keys

If you are comfortable with SSH keys, you can add them to GitHub and use SSH instead of HTTPS.

GitHub docs:

https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account

When cloning or updating the remote URL in this case, use the **SSH** URL from the **Code** dialog.

---

## END OF GIT FUNDAMENTALS LABS (Markdown Edition)
