# git Tips

## 直前の状態に戻す

コミットする前の状態で、ファイル(ディレクトリ)を直前のコミットの状態に戻したいとき:

```bash
$ git checkout -- file_or_directory_name
# すべてを元に戻したい場合
$ git checkout -- .
```

## ブランチの切り忘れ

```bash
$ git stash
$ git checkout -b branch_name
$ git stash pop
```

## `git add`したファイルをステージから削除

`git add`したファイル自体は残してコミットには含めない

```bash
$ git rm --cached file_name
```

## コミットを1つにまとめる

直近のいくつかのコミットを1つにまとめる。  
以下のような場合を想定:

```
* 4999520 コミット3
* fbe2de7 コミット2
* 6669c6b コミット1
* :tada: initial commit
```

コミット2とコミット3をコミット1にまとめる。  
その際のコミットメッセージはコミット1のものになる。  
ただし、コミットメッセージは`git commit --amend`で編集できる。  

```bash
$ git reset @~2
$ git commit --amend --no-edit
```
