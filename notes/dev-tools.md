# Development tools

- [To content](#readme.md)

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
setup git
download git (both mac and win)
download terminal
for ru version (if needed): environment => set LC_ALL=ru_RU.UTF-8 and set LANG=ru_RU.UTF-8
git line endings
set inside .gitattributes file
*.md text for text file to be converted CRLF (win) => LF (macOS, linux)
*.png binary for -text -diff macros
config git
git config --global user.name "<name>"
git config -g user.email "<email>"
git config --list stored in the user's dir .gitconfig file path: ~/.gitconfig
git init to add git to current folder
git commands (general)
git help <command>
git status
git add . dir current add to index files for commit
git add <path-to-file> add particular file(s)
git commit -m "<message>" creates a save
git commit --amend -m "<message>" to correct the last commits message (amend changes hash)
git checkout <commit hash> switches to commit, shows log till this commit
git cat-file -p <commit hash> shows commit file content -p readable format
git diff
git diff --staged indexed files
git log history
git log --oneline
git log --all shows the whole log
git log --graph
git log -1<2/3/4...> shows only 1/2/3/4/... last commits
git show <commit hash> to show the content of the commit
git checkout <file> for not commited, reset file to last commit, even if the file was deleted, can't reverse this command
git checkout <commit hash> <file> resets file to the state in the commit
git reset HEAD <file> to unstage indexed, but not yet commited file
git rm <file> and git commit --amend --no-edit removes file from commit and deletes from folder
git rm --cached <file> and git commit --amend --no-edit removes file from commit and keeps unstaged in folder
git branches
git checkout -b <pointer name> <comment hash> or without hash for current commit, creates a pointer to commit
HEAD indicates current state (where we currently are)
when we create a new commit in a branch, the pointer jumps to the last commit
git merge <pointer-to-merge> -m "<message>" creates a merge commit, the pointer will be current branch
git push origin <what-to-push>:<where-to-push>
git push :<where-to-push> to remove branch
git branch -m <name> to rename current branch
git fetch origin to get all branches from repo
git checkout -b <new-pointer-name> origin/<branch-name> to create a new branch from existing pointer
git branch --set-upstream-to=origin/<name> to link current branch to repo branch
git branch -vv to show links between branches
set SSH and integrations
git remote add origin <git@github.com...> to link remote and local repos
git remote -v shows remote repos
git push -u origin master
mkdir ~/.ssh creates a folder in user's folder, create an SSH key in this folder
ssh-keygen -t rsa -b 4096 -C "<email@email.com>" where -t rsa sets key type and -b 4096 sets key length (bit)
store private key only on your computer
load public key to repo
cat <key>.pub copy content to github
ssh -T -i ~/.ssh/<key> git@github.com to check if the key works
ssh -T git@github.com permission denied?
~/.ssh/config for settings (also using the appropriate private key)
add to the file
Host github.com
    IdentityFile ~/.ssh/key

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