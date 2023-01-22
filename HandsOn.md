# Git Hands-On

## 1. Help

```powershell
git help                        # General help
git help --guide                # Common Git guides
```

## 2. Configuration

```powershell
git help config                 # See FILES section
git config --global --list      # ~/.gitconfig

# Check specific config values
git config user.name
git config user.email
git config --global user.email git@example.com
git config --global --edit      # Open config in editor
```

## 3. Git 101

```powershell
mkdir git-hands-on
cd git-hands-on

# Create a new repository
git init git101
cd git101
ls .git

# - .git/objects/               (empty)
# - .git/refs/heads/            (empty)
# - .git/config                 `git config -e`
# - .git/HEAD                   ref: refs/heads/master

git status
touch README.md                 # Create README.md

git status                      # Untracked files!
git add -A                      # Track all changes

git status                      # Changes!
    # <internals>
    ls .git/objects/
    ls .git/objects/e6/
    git cat-file -t e69de29bb2d1d6434b8b
    # </internals>
    
git commit -m "Add empty README"
    # <internals>
    git cat-file -t f93e3a1a1525fb5b9102
    git cat-file -p f93e3a1a1525fb5b9102
    cat .git/HEAD
    ls .git/refs/heads/
    cat .git/refs/heads/master
    git rev-parse HEAD
    git cat-file -p $(git rev-parse HEAD)
    # </internals>
    
git show HEAD
git log
```

### Git 101 Summary

1. Make changes
2. Track changes: `git add -A`
3. Commit changes: `git commit -m "Do something"`

## 4. Clone a Remote Repository

```powershell
cd ..
git clone https://github.com/indramahkota/learn-git.git learn-git

cd learn-git
ls .git

git status
    # <internals>
    git cat-file -p $(git rev-parse HEAD)
    git cat-file -p "HEAD^{tree}"
    git cat-file -p 176a458f94e0ea5272ce
    # </internals>
    
git branch
git remote -v
git branch -r

git config branch.gh-pages.remote
git config branch.gh-pages.merge

gitk
```

## 5. Push to a Remote Repository

```powershell
git commit -am "Fix favorite number"

git status                      # Branch is ahead

gitk

git log --oneline --graph --decorate
git config --global push.default upstream

git push
```

```powershell
git remote set-url origin https://github.com/indramahkota/learn-git.git
git push
```

## 6. Working Locally with Branches

```powershell
git branch feature1             # Create branch from here
git checkout feature1           # Switch to different branch
    # <internals>
    cat .git/HEAD
    cat .git/refs/heads/feature1
    # <internals>
    
git status
touch feature1.md
git add .
git commit -m "Add feature 1"
    # <internals>
    cat .git/HEAD
    cat .git/refs/heads/feature1
    # <internals>

touch feature2.md
git add .
git status

git checkout gh-pages -q
git checkout -b feature2
git commit -m "Add feature 2"
gitk --branches

git checkout gh-pages -b feature3
touch feature3.md

touch feature4.md

git add .
git status

git reset feature4.md           # reset path is opposite of add
git status
git commit -m "Add feature 3"
git checkout gh-pages -b feature4
git add .
git commit -m "Add feature 4"
gitk --branches
```

## 7. Working Remotely with Branches

```powershell
git remote add upstream https://github.com/indramahkota/learn-git.git
    # <internals>
    ls .git/refs/remotes/
    # </internals>
    
git fetch --all
    # <internals>
    ls .git/refs/remotes/upstream/
    cat .git/refs/remotes/upstream/gh-pages
    # </internals>

git push origin feature1

git push origin HEAD

git status

git push

git push -u origin HEAD
git status

git push

git config --global alias.pc "push -u origin HEAD"
git pc

git branch -r
git fetch --all

git remote prune origin
git fetch --prune --all

git status                      # upstream is gone!
git branch -d feature4
git branch -D feature4

git checkout feature1
git status                      # behind!
git pull                        # get latest & merge

git checkout --track origin/feature5

git checkout master
git branch -D feature5

git checkout feature5

touch feature5
git add .
git commit -m "Add feature5"
git push
```

## 8. Merging

```powershell
git checkout feature1

git reset --hard HEAD~
gitk feature1 origin/feature1

git merge --no-ff origin/feature1

git merge feature2

git reset --hard HEAD~2
git merge origin/feature1 feature2 feature3
```
