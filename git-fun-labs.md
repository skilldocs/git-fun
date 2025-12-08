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
git commit -am "COMMIT_MSG"
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

### 1. Add another change.

Let’s first make another change to the repository to make the history more interesting. Add a line to the first file you committed into the repository and then stage and
commit. Note that you can use the shortcut here.

```bash
echo new >> FILE1
git commit -am "COMMIT_MSG"
```

<br><br>

### 2. View history.

Now, take a look at the history we have so far in our small repository. To do this we just run the *log* command.

(Note: In some terminals your history may be longer than the screen and need to hit a key to continue. If you are paging through log output and want to end the listing, hit the “q” key.)

```bash
git log
```

<br><br>

### 3. View one-line history.

Often when looking at Git history information, users will only want to see the first line of each entry - the “subject line”. This is why it is important to make that first line meaningful in a real-life use of Git. To see only the first line of each log message, you can use the *--oneline* option.

```bash
git log --oneline
```

<br><br>

### 4. Use formatted log output.

Let’s try a more complex version of the log command that includes selected pieces of history information formatted in a specific way. Be careful of your typing - note the colon after “format”, the double hyphens, and the double quotes.

```bash
git log --pretty=format:"%h %ad|%s %d[%an]" --date=short
```

<br><br>

### 5. Create a helpful alias for the formatted history.

Since this is a bit much to type, let’s create an alias to simplify running this command. We do this by configuring the alias name to stand for the command and its options. Enter the following, paying attention to the punctuation (double hypens, colon, vertical bars, single and double quotes, etc.)

```bash
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --date=short"
```

<br><br>

### 6. Run the alias.

Now run your new *hist* alias. You should see the same output as the original *log* command from step 3. If you encounter any problems, go back and double-check what you typed in step 4.

```bash
git hist
```

<br><br>

### 7. Show history for a single file.

We can also use the log command (and our hist alias) on individual files. Pick one of your files and run the hist alias against it.

```bash
git hist FILE1
```

<br><br>

### 8. Identify earliest & latest commit SHAs.

Question: We're interested in seeing the differences between a couple of the revisions. But there are no version numbers. How do we pick revisions?
Answer: We pick revisions via the SHA1 (hash) values (first 7 bytes are enough). It's the first column in the *hist* output.

Run:
```bash
git hist
```

Note the SHA of:
- The earliest commit (bottom of the list)
- The latest commit (top of the list)

![list of commits](./images/git3.png?raw=true "List of commits") 

<br><br>

### 9. View history between two SHAs.

We can use these SHA1 values similarly to how we might use version numbers in other systems. Let’s see the history between our earliest and latest commits.

To do this, we’ll run the hist alias and specify the range of values using the SHA1 values. Execute the command below, substituting the appropriate SHA1 values from the history in your repository.

```bash
git hist EARLIEST_SHA1..LATEST_SHA1
```

<br><br>

### 10. View diff for a file across that range.

You should see a similar history as you saw previously. One thing to note here is you don’t see the original (first) commit. This is because when specifying ranges via the “..” syntax, Git defines that as essentially everything after the first revision. Note that you can also run this against an individual file. Try the command below with your SHA1 values and the first file you added in the repository

```bash
git diff EARLIEST_SHA1..LATEST_SHA1 FILE1
```

<br><br>

### 11. Create tags for earliest and latest commits.

Finding and typing SHA1 values each time for operations like this can be cumbersome. To simplify this, we can use tags to point to commits, and then use those tag names instead of the SHA1 values in commands. Let’s create tags for the earliest and latest commits in our repository. We’ll use the tags *first* and *last* respectively. The commands are below.

```bash
git tag first EARLIEST_SHA1
git tag last LATEST_SHA1
```

<br><br>

### 12. Use tags instead of SHAs in history commands.

Now that we have the tags, we can use them anyplace we used the SHA1 values before. Try out the hist alias with the tags.

```bash
git hist first..last
```

<br><br>

### 13. Show filenames that changed using the range specified by the tags.

This is giving us the history for all of the files in the repository. This is because a tag applies to an entire commit - not a specific file in the commit. To see this more clearly, add the --name-only option to the command and run it again.

```bash
git hist first..last --name-only
```
<br><br>

### 14. Filter by file.

If we only want to do an operation using a tag for one file, we can simply add that filename onto the command. Try out the example below.
```bash
git hist first..last --name-only FILE1
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

### 1. View existing branches.

Starting in the same directory as you used for Lab 3, take a look at what branches you have currently with the git branch command.

```bash
git branch
```

<br><br>

### 2. Interpret the branch list.

You should see:
- `* main` — only one branch, and `main` is the current branch.

<br><br>

### 3. Update a file on `main`.

Before we work with a new branch, let’s update at least one file in the `main` branch to indicate that this is the version on main so it will be easier to
see which version we have later. To do this, we can just use a short version of the same way we have been creating and updating other files. Stage and commit it with the shortcut.

```bash
echo "main version" >> EXISTING_FILE
git commit -am "main version"
```

<br><br>

### 4. Create a feature branch.

We have a new feature to work on, create a branch for the feature. 

```bash
git branch FEATURE_BRANCH
```

<br><br>

### 5. Verify branches

Notice that the previous command created the branch but *did not switch* to it. Let’s check what branches we have and which is our current one.

```bash
git branch
```

You should now see:
- `main`
- `FEATURE_BRANCH`

<br><br>

### 6. Switch to the feature branch. 

We can now see our new branch listed. Let’s change into the `feature` branch to do some work.

```bash
git checkout FEATURE_BRANCH
```
<br><br>

### 7. Verify you are on the feature branch.


```bash
git branch
```
The `*` should now be next to `FEATURE_BRANCH`.

<br><br>

### 8. Create a new file on the feature branch.

```bash
echo some-text > NEW_FILE
```

<br><br>

### 9. Update an existing file to indicate that it is associated with the feature branch.

```bash
echo "feature version" >> EXISTING_FILE
```

<br><br>

### 10. Stage and commit your changes.

```bash
git add .
git commit -m "feature version"
```

<br><br>

### 11. Switch back to `main`.

```bash
git checkout main
```

<br><br>

### 12. Verify you're on `main`

```bash
git branch
```

You should see `* main` in the branch list.

<br><br>

### 13. Check file contents on `main`.

Take a look at the contents of the files and verify that they're the original ones from main.

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

### 1. Verify clean working state.
```bash
git status
```
You should see: `working tree clean`.

<br><br>

### 2. Create a new *one-line* file on `main` with a line that identifies it as the `main` version.

```bash
echo some-text > NEWFILE
```

<br><br>

### 3. Stage and commit the new file on `main`.

```bash
git add .
git commit -m "adding new file on main"
```

<br><br>

### 4. Create a new branch (but do not switch to it yet).

```bash
git branch NEW_BRANCH
```

<br><br>

### 5. Change the same line in the new file on `main`.

```bash
echo "Update on main" > NEWFILE
```

<br><br>

### 6. Stage and commit the change on `main`

```bash
git add .
git commit -m "update on main"
```

<br><br>

### 7. Switch to `new-branch`

```bash
git checkout NEW_BRANCH
```

<br><br>

### 8. Change the same line in the same file on `NEW_BRANCH`

```bash
echo "Update on NEW_BRANCH" > NEWFILE
```

<br><br>

### 9. Commit the change on `NEW_BRANCH`
```bash
git commit -am "update on NEW_BRANCH"
```

<br><br>

### 10. Switch back to `main`
```bash
git checkout main
```

<br><br>

### 11. Merge `new-branch` into `main`

```bash
git merge NEW_BRANCH
```

<br><br>

### 12. Check status for conflicts. 

What is the status info that tells us we have a merge conflict?

```bash
git status
```

<br><br>

### 13. Inspect the conflict markers.

```bash
cat NEWFILE
```

You should see conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`).

<br><br>

### 14. *Fix* the conflict.

For simplicity, just overwrite the file with a merged version:

```bash
echo "merged version" > NEWFILE
```

<br><br>

### 15. Stage and commit the resolved file.

```bash
git commit -am "Fixed conflicts"
```

<br><br>

### 16. Verify the merge is complete

```bash
git status
```

<br><br>

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
