# Development tools

## Chrome Dev Tools
<details>
<summary>Shortcuts and tips</summary>

- Shortcuts (menu => shortcuts)
  - `ctrl + F` search (by any word)
  - `ctrl + shift + F` search across all sources
  - `tab` `tab + shift` step forward / back when adding changes
  - `H` hide chosen element of the html (adds `visibility: hidden;`)
  - `F2` to be able to edit html
  - `+` in styles will create a selector for the element
  - `shift + click` on color will change it's output
- `document.body.contentEditable = true;`
- can change sizes in the block with metrics
- in the device emulation can pick pixel density
- settings => coverage lets to see all the rules, which are not applied to the page

</details>

## Git and GitHub
- setup git
  - download git (both mac and win)
  - download terminal
  - for ru version (if needed): `environment` => `set LC_ALL=ru_RU.UTF-8` and `set LANG=ru_RU.UTF-8`
- git line endings
  - set inside `.gitattributes` file
  - `*.md text` for text file to be converted `CRLF` (win) => `LF` (macOS, linux)
  - `*.png binary` for `-text -diff` macros
- config git
```bash
git config --global user.name "<name>"
git config -g user.email "<email>"

# stored in the user's dir .gitconfig file path: ~/.gitconfig
git config --list

# to add git to current folder
git init
```
- git commands (general)
```bash
git help <command>
git status

# dir current add to index files for commit
git add .
# add particular file(s)
git add <path-to-file>
# creates a save
git commit -m "<message>"
# to correct the last commits message (amend changes hash)
git commit --amend -m "<message>"
# switches to commit, shows log till this commit
git checkout <commit hash>
# shows commit file content -p readable format
git cat-file -p <commit hash>

git diff
# indexed files
git diff --staged

# history
git log
git log --oneline
# shows the whole log
git log --all
git log --graph
# shows only 1/2/3/4/... last commits
git log -1<2/3/4...>
# to show the content of the commit
git show <commit hash>

# for not commited, reset file to last commit, even if the file was deleted, can't reverse this command
git checkout <file>
# resets file to the state in the commit
git checkout <commit hash> <file>
# to unstage indexed, but not yet commited file
git reset HEAD <file>
# these 2 commands remove file from commit and delete from folder
git rm <file>
git commit --amend --no-edit
# these 2 commands remove file from commit and keep unstaged in folder
git rm --cached <file>
git commit --amend --no-edit
```
- git branches
- `HEAD` indicates current state (where we currently are)
- when we create a new commit in a branch, the pointer jumps to the last commit
```bash
# or without hash for current commit, creates a pointer to commit
git checkout -b <pointer name> <comment hash>
# creates a merge commit, the pointer will be current branch
git merge <pointer-to-merge> -m "<message>"
git push origin <what-to-push>:<where-to-push>
# to remove branch
git push :<where-to-push>
# to rename current branch
git branch -m <name>
# to get all branches from repo
git fetch origin
# to create a new branch from existing pointer
git checkout -b <new-pointer-name> origin/<branch-name>
# to link current branch to repo branch
git branch --set-upstream-to=origin/<name>
# to show links between branches
git branch -vv 
```
- set SSH and integrations
```bash
# to link remote and local repos
git remote add origin <git@github.com...>
# shows remote repos
git remote -v
git push -u origin master
```
- store private key only on your computer
- load public key to repo
```bash
# creates a folder in user's folder, create an SSH key in this folder
mkdir ~/.ssh
# where -t rsa sets key type and -b 4096 sets key length (bit)
ssh-keygen -t rsa -b 4096 -C "<email@email.com>"
# copy content to github
cat <key>.pub
# to check if the key works
ssh -T -i ~/.ssh/<key> git@github.com
# permission denied?
ssh -T git@github.com
# for settings (also using the appropriate private key)
~/.ssh/config
# add to the config file
Host github.com
    IdentityFile ~/.ssh/key
```

## Terminal
pwd full path to current dir
cd change dir
cd - to previous folder
mkdir name and touch name creates a dir or file
ls <path/to>
ls -1 vertically
ls -a +hidden
open . or start . or instead of . add path to open dir or file
cat <file> shows the content