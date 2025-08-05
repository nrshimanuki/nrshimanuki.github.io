Git
===

## Install

* [https://git-scm.com/download/mac](https://git-scm.com/download/mac)

```
brew install git

git --version
```

## Change default branch name

```
git config --global init.defaultBranch main
```


## Name and E-mail

```
git config --global user.name 'global'
git config --global user.email 'global@example.com'

git config --local user.name 'local'
git config --local user.email 'local@example.com'
```


## Color setting

```
git config --global color.ui auto
```


## Quick setup

```
cd
cd xxxxx/xxxxx

wget https://raw.githubusercontent.com/github/gitignore/master/WordPress.gitignore -P ./
mv WordPress.gitignore .gitignore

git init
git add .gitignore
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/nrshimanuki/xxxxx.git
git push -u origin main
```


## Commands

### Clone repository
```git clone https://github.com/nrshimanuki/xxxxx.git```

### Push
```
git add --all
git commit -m "Comment"
git push
```

### Pull
```git pull origin main```

### Restore working tree files
```
git checkout HEAD .
git checkout .
```
### Revert some existing commits
```git revert <commit>```

### List branches
```git branch```

### Create a new bran
```
git branch <branch name>
  or
git checkout main
git checkout -b <branch name>
```

### Change branch
```git checkout <branch name>```

### Delete branch
```git checkout -d <branch name>```

### Merge
```
git checkout main
git merge develop
```

#### __Ex__
```
git add --all
git commit -m "modified"
git push -u origin develop
git checkout main1
git merge develop
git push -u origin main
git checkout develop
git branch
```

## Rebase
```
git checkout main
git pull origin main
git checkout hoge
git rebase main

git add 〜
git rebase --continue

git push -f origin hoge
```

1. rebaseしたいブランチを最新にする
2. 作業ブランチに戻る
3. rebaseする (git branch で確認すると一時的なブランチにいる)
4. コンフリクトが発生したら解決する
5. リモートのoriginと相違している状態になったためpushしようとするとエラーになるので、-fで強制的にpushする
