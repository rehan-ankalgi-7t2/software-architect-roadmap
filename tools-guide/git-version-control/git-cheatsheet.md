# Git For Professionals
## Optimised Staging

### Add all the local changes in the project to staging area

```bash
git add .
```

### Add “Patched” changes as code blocks / chunks to the staging area

```bash
git add -p filename.ext
```

### Writing meaning full commit messages

```bash
git commit
```

opens up a text editor to write the commit message along with the body

![Screenshot 2023-04-28 at 11.40.36 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a43fd100-9974-4902-a515-c713cea324ed/Screenshot_2023-04-28_at_11.40.36_AM.png)

```bash
git commit -m "...message goes here"
```

for writing one liner commit messages in the terminal

## Branching Strategies

### Need for a convention to follow is that git provides the tool but doesn’t provide a way to use it

![Screenshot 2023-04-28 at 11.45.58 AM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4462b08c-eb23-4afd-9585-7c62a377843f/Screenshot_2023-04-28_at_11.45.58_AM.png)

### Types of branches

- long running branch (main / master / development / production / staging)
- short run branch (feature / refactoring / bug fix)

### Long-running branch

- exist throughout the complete lifetime of the project
- often, they mirror stages in your dev life cycle
- common convention in these branches - “no direct commits”, changes are done only with integration like merging or rebase

### Short-lived branch

- for new features, experimentation, refactoring, bug fixes etc
- will be deleted after integration (merge / rebase)

## Github flow branching strategy

- very simple
- lean
- only one - long running branch “main / master”
- rest are feature branches or short lived branches

### Create a branch

```bash
git branch branch-name

example: git branch test
```

### Change the branch

```bash
git checkout branch-name

example: git checkout test
```

# Pull Requests ⤵️

## Steps to be followed to contribute to a repository  on github

### Step1 - fork the repository  to your github account

![Screenshot 2023-04-28 at 12.17.44 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/326512d1-0bcc-4df6-b858-ac491c410a57/Screenshot_2023-04-28_at_12.17.44_PM.png)

### Step 2 - clone the repository to your local machine

```bash
git clone repository-link

example: git clone https://github.com/rehan-ankalgi-7t2/DSA-java.git
```

### Step 3 - Make changes

now “cd” into the cloned repository and make the changes, add your features and make a local commit to “your” branch.

to commit changes to your branch follow the below steps

Add the changes to the staging area

```bash
git add filename.ext

OR

git add -p filename.ext
```

Write a meaningful commit message

```bash
git commit

OR

git commit -m "...message"
```

push code your forked repository on your branch

```bash
git push -u origin branch-name

example: git push -u origin test
```

### Step 4 - open a pull request on the main repository

![Screenshot 2023-04-28 at 12.39.15 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8c58ffb3-cebf-4133-9cb9-92ae8b1bf21e/Screenshot_2023-04-28_at_12.39.15_PM.png)

![Screenshot 2023-04-28 at 12.39.51 PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6a414651-b2ad-4346-ab9e-46ccf8b92735/Screenshot_2023-04-28_at_12.39.51_PM.png)

# Merge Conflicts ☠️

<aside>
💡 when do merge conflicts occur?

</aside>

- when integrating commits from a different source
- when contradictory changes happen

### Merging

```bash
git merge branch-name

example: git merge develop
```

### Undo a merge conflict

```bash
git merge --abort
```

```bash
git rebase --abort
```

### How to resolve merge conflicts?

- clean up the file that is creating the merge conflict
- use merging tools configured using git config

# Merge .vs. Rebase .vs. Squash
Git offers three main strategies for integrating changes from one branch to another: `Merge`, `Rebase`, and `Squash`. Each strategy has its advantages and is suitable for different scenarios. Let’s understand the differences and how to choose the right one:

[![Git MERGE vs REBASE: Everything You Need to Know](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/0chZFIZLR_0?si=Aqsa2Bhuol47F2Q9)
    
### 1. Git Merge
![alt text](https://miro.medium.com/v2/resize:fit:720/format:webp/0*qS37ldEO_QdD4OLU.png)
— Merge integrates the entire history of one branch into another, including all the individual commits from the feature branch. It creates a new commit on the target branch, known as a “merge commit.”
— This strategy is simple and easy to understand. It’s commonly used, especially for updating feature branches that are shared among team members.
— However, the history becomes cluttered with merge commits, and debugging with “git bisect” can be more challenging due to the extra commits.

### 2. Git Rebase
![alt text](https://miro.medium.com/v2/resize:fit:720/format:webp/0*W28uicsv40QTx7vx.png)
— Rebase rewinds the commits from the feature branch and replays them on top of the latest commit from the target branch. It creates new commit hashes for each commit in the feature branch.
— It results in a cleaner commit history since it avoids merging commits. However, if the feature branch is shared with others, it’s generally not recommended as it can lead to broken repositories for others.
— Rebase helps identify conflicts sooner, as they are resolved while replaying the changes onto the target branch.


### 3. Git Squash
![alt text](https://miro.medium.com/v2/resize:fit:720/format:webp/0*W28uicsv40QTx7vx.png)
— Squash combines all the individual commits from the feature branch into a single commit with a new commit message. It doesn’t carry over the commit history from the feature branch.
— This strategy is useful when you want to merge the feature branch changes as a single commit, making it easier to track and find changes if needed.
— Squash is typically used in combination with `Merge` or `Rebase`.


Choosing the Right Strategy:
The strategy you choose depends on the specific scenario:

Merge
— Use Merge when updating a shared feature branch to avoid recalculating commit hashes that could lead to conflicts for others.
— Use Merge when updating a feature branch that is significantly behind the target branch, as resolving conflicts during rebase might be more difficult.

Rebase
— Use Rebase when updating a feature branch that is not shared with others. It keeps the branch history clean and easier to manage.

Squash
— Use Squash when merging feature branch changes into the target branch. It creates a single commit for all the changes, making it easier to track.