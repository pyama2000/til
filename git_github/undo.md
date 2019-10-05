# Gitで変更をあれこれする方法

## 変更を保存(スタッシュ)してあとで使う

> `git stash`   

### スタッシュする

```bash
# 追跡していて、変更があったファイル(unstageなファイル)をスタッシュ
$ git stash
$ git stash push # 以前は`save`だったが廃止され、今は`push`に変更された

# 追跡していないファイルもスタッシュ
$ git stash -u

# メッセージを付けてスタッシュ
$ git stash -m "stash message"
```

### スタッシュを適用する

```bash
# 適用したスタッシュは残す
$ git stash apply

# 適用したスタッシュを破棄
$ git stash pop
```

## 変更したファイルを直近のコミットに含める

> `git commit --amend`

変更したファイルを`git add`して直近のコミットに含める、または、コミットメッセージを変更する場合に使用。

```bash
# コミットメッセージを上書きして直近のコミットに含める
$ git commit --amend -m "commit message"

# コミットメッセージは編集せずに直近のコミットに含める
$ git commit --amend --no-edit
```

### 注意

もし他の人がリモートにプッシュしていた場合、`git push --force`を実行する必要がある。

## 参考
> [Undo changes in Git - Cheat sheet for git checkout, stash, reset, clean, revert, rebase -i, amend](https://dev.to/mzanggl/undo-changes-in-git-cheat-sheet-for-git-checkout-stash-reset-clean-revert-rebase-i-amend-2h1h?utm_source=digest_mailer&utm_medium=email&utm_campaign=digest_email#dont-undo-save-changes-for-later-use)  