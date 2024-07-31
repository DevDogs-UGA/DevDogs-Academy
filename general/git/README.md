### Outline/TODO

- [x] What is Git
- [x] Key Terms
    - [ ] Repository
    - [ ] Commit
    - [ ] Branch
- [ ] Commands
    - [x] git config
    - [x] git init
    - [x] git clone
    - [ ] git checkout
    - [ ] git branch
    - [ ] git add
    - [ ] git status
    - [ ] git commit
    - [ ] git push
    - [ ] git log
    - [ ] git fetch
    - [ ] git pull
    - [ ] git merge
    - [ ] git rebase


# What is Git
Git is a free and open-source version control system created by Linus Torvalds. It tracks and manages changes in your code and makes it easier to collaborate on projects with others. Git allows users to see who made what changes when and easily revert to older snapshots of a project. We use it to avoid having to store multiple versions of files. Git handles everything in an effecient way. 


# Key Terms
**Repository (AKA repo)** - A folder where are the files being tracket by git are located. It's also where the `.git` folder is located which contains all the meta data.

**Commit** - A commit is when you take a snapshot of changes made to your repository. Commits are logged and and used to track and manage the history of your repository.

**Branch** - A branch is an offshoot from the main line of development. It's like a safe zone where you can commit changes without affecting the main line. This is especially useful when working with others because you can experiment and make changes without interfering with code others are working on. When you are done making changes you can merge your changes into the main line of development.

<img src="./media/branch-visual.png" alt="Branch Visual Image" width="200"/>
<img src="./media/branch-merge-visual.png" alt="Branch Merge Visual" width="200"/>

Left,visualization of branching. Right, visualization of merging the branch.

# Commands

### git config
`git config` is used to set your repository's configuration values. You can set config values either locally or globally. Local settings only affects the current repository you are working on. Global settings apply on all git repos. Local settings overwrite global settings. The most common usage is setting your name and email.

This command sets your global email

`git config --global user.name your.email@service.com`

and this one sets your global name

`git config --global user.name yourName`

This is so people know who made what changes. Without a name and email you will not be able to apply changes.

To list your config settings (located in `.git/config` in your repo folder) run `git config --list`.

---
### git init

All `git init` does is initialize your github repository. If you run `git init` in a folder it adds a .git folder which includes all of the meta data needed to start using git for your files.

---
### git clone

`git clone URL` copies a remote repository and all of it's history onto your computer. Git supports https, git, and ssh protocols for the URL.

### git checkout
`git checkout branchName` switches you to the branch you specify.

`git checkout -b branchName` creates the branch given and then switches you to it.

---
### git branch
