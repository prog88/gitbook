# [cheatsheet] GIT 

## Dotfiles

* A file including names of stuff that you don"t want to be staged or tracked. You usually keep your local files like database, media, and etc here. You can find good resources online about ignoring specific files in your project files. `.gitignore` is also get ignored.

`.gitignore`

* A hidden directory in repo directory including git files. It is created after "git init". Usefull for hooks :)

`.git`

## Usage

* initiates git in the current directory:

`git init`

* creates a git repo from given address (get the address from your git-server). It could be from `https|ssh`. I personally mostly use `ssh` way:

`git clone <address>`

* shows the modifications and stuff that are not staged yet:

`git status`

* show the differences between two branches:

`git diff`

* adds(stages) `readme.md` to the git:

`git add readme.md`

* adds(stages) all new modifications, deletions, creations to the git:

`git add *`

* removes `readme.md` from the stage:

`git reset readme.md`

* removes `readme.md` both from git and file system:

`git rm readme.md`

* removes untracked files or directories. _Always be aware when using `-f` in command line_:

`git clean -df`

* undoes all commmit after a commit_id, preserving local changes:

`git reset [#commit]`

* discoard all history and changed back to the specified commit. (When git reset is not enough):

`git reset --hard [#commit]`

## Branch 

* shows all the branches (current branch is shown with a star):

`git branch`

* creates `my-branch`:

`git branch my-branch`

* deletes `my-branch`:

`git branch -d my-branch`

* switches to `my-branch`:

`git checkout my-bracnch`

* merges my-branch to current branch:

`git merge my-branch`

* delete remote branch:

`git push origin :my-branch`

## Cherry pick

* merge the specified commit providing a commit_id:

`git cherry-pick [commit_it]`

## Remote

* shows the remotes:

`git remote`
 
* shows the remote for pull and push:

`git remote -v`

* creates a remote (get the address from your git-server):

`git remote add my-remote [address]`

## Log

* shows the log of commits:

`git log`

* commit changes with a descriptive short message (*)[Tips & Trick](#tips-n-tricks):
 
 `git commit -m "changing this for that to fix this specific issue"`
 
 * pushes the commits to the my-remote in my-branch (does not push the tags), `-u` could be use to push 'upstream':

`git push my-remote my-branch`

* rewrite the very last commit with any currently staged changes. *(Works for commits that have not pushed to re remote repo)*:

```
git add .
git commit --amend -m "Update roles for netlify-cms git gateway"
```

## Tag

* shows all the tags:

`git tag`

* creates an annotated tag:

`git tag -a v1.0.0 -m "msg"`


* shows the description of version-1.0 tag:

`git show v1.0.0`

* deletes the tag in local directory:

`git tag --delete v1.0.0`

* deletes the tag in my-remote (be carefore to not delete a branch):

`git push --delete my-remote v1.0.0`

* push v1.0 tag to my-remote in my-branch:

`git push my-remote my-branch v1.0.0`

* pulls the tags from remote:

`git fetch --tags`

## My Remote - My Branch

* pulls and tries to merge `my-branch` from `my-remote` to the current branch:

`git pull my-remote my-branch`

## Stash

* stashes the staged and unstaged changes (git status will be clean after it):

`git stash`

* stash everything including new untracked files (but not .gitignore):

`git stash -u`

* stash with a msg:
`
git stash save "msg"`

* list all stashes:

`git stash list`

* delete the recent stash and applies it:

`git stash pop`

* delete the {2} stash and applies it:

`git stash stach@{2}`

* shows the description of stash:

`git stash show`

* keep the stash and applies it to the git:

`git stash apply`

* creates a branch from your stash:

`git stash branch my-branch stash@{1}`

* deletes the {1} stash:

`git stash drop stash@{1}`

* clears all the stash:

 `git stash clear`

## Glossary

* git: an open source, distributed version-control system.
* commit: a Git object, a snapshot of your entire repository compressed into a SHA.
* branch: a lightweight movable pointer to a commit.
* clone: a local version of a repository, including all commits and branches.
* remote: a common repository on GitHub that all team member use to exchange their changes.
* pull request: a place to compare and discuss the differences introduced on a branch with reviews, comments, integrated tests, and more...
* HEAD: representing your current working directory, the HEAD pointer can be moved to different branches, tags, or commits when using `git checkout`

## Tips n Tricks

* Commit message

Here are some tips and tricks, to improve your commit message, logs readability, also help for CI (continuous integration) tags versioning.
* Specifying without assume the reviewer understand the purpose or what the original issue was.
* The message body should explain what changes you have made and why you made them.
* By specifying your type of commit using either (feat | fix | style | refactor | test | docs | chore) as following examples:

```
- feat: The new feature you're adding to a particular application
- fix: A bug fix
- style: Feature and updates related to styling
- refactor: Refactoring a specific section of the codebase
- test: Everything related to testing
- docs: Everything related to documentation
- chore: Regular code maintenance.[ You can also use emojis to represent commit types]
```

* checkout older version of file

It happends to screw up some .lock files (podfile.lock / gemfile.lock). 
Rather than reverting a commit, we can just *reset* the file back to it older version

```
git checkout hash Podfile.lock
```

* cherry-pick 

I occasionally use. It's sometime easier to get just what we need rather than try to get
the entire branch up.
To following commits over to the branch we are on.

```
git cherry-pick first-hash second-hash third-hash
``` 

or range syntax

```
git cherry-pick first-hash..third-hash
```

## References

* Useful link for basics to advanced usage of [GIT](https://git-scm.com/book/en/v2)
* Very ludic website that can be sude to [learn and practice git](https://learngitbranching.js.org/)
