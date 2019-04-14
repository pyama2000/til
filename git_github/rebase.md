# `git rebase`について

## `rebase`の役割

`rebase`コマンドはブランチを統合する機能がある。
しかし、ブランチの統合以外にも様々な機能がある。

## `rebase --interactive`

rebaseしようとする前にコミットのリストを作成し、コミットの編集を行う。
以下のようなコミットを編集する。

```shell
$ git log --oneline
d9230c8 commit5
d3c1188 commit4
21d6597 commit3
9cf328e commit2
ad7f9e4 commit1
```

上記のコミットのうち、直近3つ(commit5 - commit3)を編集する。
コミットを編集するために以下のコマンドを実行する。

```shell
$ git rebase --interactive HEAD~3
```

`--interactive`は`-i`と省略可能。
また、`HEAD~3`の代わりにコミットIDを使用することも可能。
コミットIDを使用する場合、まとめるコミットの更にもう一つ前のコミットIDを引数に指定する。
今回の場合は、`9cf328e`(commit2)を指定する。

```shell
$ git rebase -i HEAD~~~
$ git rebase -i HEAD~3
$ git rebase -i 9cf328e
```

これらはすべて`$ git rebase --interactive HEAD~3`と同じである。
このコマンドを実行するとエディタが起動し、以下のような画面が表示される。

```
pick 21d6597 commit3
pick d3c1188 commit4
pick d9230c8 commit5

# Rebase 9cf328e..d9230c8 onto 9cf328e (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

コミットID、コミットメッセージの前に`pick`というコマンドがあるが、これはそのコミットをそのまま使用するという意味である。
それ以外のコマンドは以下で説明する。

### `squash`/`fixup`: コミットを統合する

`squash`と`fixup`はどちらもコミットを1つ前のコミットに統合するコマンドである。
`squash`はコミットメッセージも統合する場合、`fixup`はコミットメッセージを破棄する場合に使用する。

#### `squash`を実行した結果

commit3にcommit4とcommit5を統合しどのコミットメッセージも使用する場合。

```
pick 21d6597 commit3
squash d3c1188 commit4
squash d9230c8 commit5
```

commit4とcommit5を`pick`から`squash`に変更し、保存する。
すると、以下のような画面が表示される。

```
# This is a combination of 3 commits.
# This is the 1st commit message:

commit3

# This is the commit message #2:

commit4

# This is the commit message #3:

commit5

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Sun Apr 14 23:25:34 2019 +0900
#
# interactive rebase in progress; onto 9cf328e
# Last commands done (3 commands done):
#    squash d3c1188 commit4
#    squash d9230c8 commit5
# No commands remaining.
# You are currently rebasing branch 'test' on '9cf328e'.
#
# Changes to be committed:
#	modified:   test.md
#
```

このように統合するコミットのコミットメッセージが編集できる。
このまま保存すると以下のようなログになる。

```shell
$ git log
commit 14893aa9f45c16275d8391ec231dc9d19dd4bda9 (HEAD -> test)
Author: xxx <xxx@xxx.com>
Date:   Sun Apr 14 23:49:30 2019 +0900

    commit3

    commit4

    commit5

commit 9cf328e221ceadcc6ae822d856b4c3fd7c702c6c
Author: xxx <xxx@xxx.com>
Date:   Sun Apr 14 23:25:20 2019 +0900

    commit2

commit ad7f9e4ecc3132fb621fc0ffa82bb0965bb0a6a8
Author: xxx <xxx@xxx.com>
Date:   Sun Apr 14 23:25:00 2019 +0900

    commit1
```

#### `fixup`を実行した場合

commit3にcommit4とcommit5を統合しどちらのコミットメッセージも破棄(commit3のコミットメッセージのみを使用)する場合。

```
pick df99a59 commit3
fixup 4722245 commit4
fixup 81affae commit5
```

```shell
$ git log
commit 67b6d7bbea65a79ff06135581151e4372610f8f3 (HEAD -> test)
Author: xxx <xxx@xxx.com>
Date:   Sun Apr 14 23:49:30 2019 +0900

    commit3

commit 9cf328e221ceadcc6ae822d856b4c3fd7c702c6c
Author: xxx <xxx@xxx.com>
Date:   Sun Apr 14 23:25:20 2019 +0900

    commit2

commit ad7f9e4ecc3132fb621fc0ffa82bb0965bb0a6a8
Author: xxx <xxx@xxx.com>
Date:   Sun Apr 14 23:25:00 2019 +0900

    commit1
```
