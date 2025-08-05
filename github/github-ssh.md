SSHを使用した接続
===============

## 概要・前提

* GitHub に push ができるように SSH を設定する
* GitHub のアカウントは仕事用とプライベート用が存在するので SSH key を分ける


## 手順

* SSH鍵をそれぞれ作成する
* GitHubに公開鍵を登録する（各アカウントに）
* ~/.ssh/config ファイルを設定して使い分ける
* リポジトリごとに適切なホスト名（エイリアス）を使ってクローンまたはプッシュする


## SSH key をそれぞれ作成

```
ssh-keygen -t ed25519 -C "work@example.com" -f ~/.ssh/github/id_ed25519_work

ssh-keygen -t ed25519 -C "private@example.com" -f ~/.ssh/github/id_ed25519_private
```

* -C のメールアドレスは識別用のコメントなので実際のGitHubアカウントのメールと一致しなくてもOK。
* -f は鍵ファイルの保存場所。デフォルトの ~/.ssh/id_ed25519 以外を指定。


## 公開鍵を GitHub に登録

以下で表示して、GitHub のアカウント設定から「SSH and GPG keys」に追加 (.pub)

```
cat ~/.ssh/github/id_ed25519_work.pub

cat ~/.ssh/github/id_ed25519_private.pub
```

## ~/.ssh/config を編集

```
## 仕事用
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github/id_ed25519_work
  IdentitiesOnly yes

## プライベート用
Host github.com.private
  HostName github.com
  User git
  IdentityFile ~/.ssh/github/id_ed25519_private
  IdentitiesOnly yes
```


## SSH接続の確認

```
ssh -T git@github.com
ssh -T git@github.com.private

> Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```


## clone

```
git clone git@github.com:your-username/your-repo.git

git remote add origin git@github.com:GithubUserName/YourRepositoryName.git
```
