# 開発用の環境構築

## パッケージ管理・仮想環境

### Pyenv

### Pipenv

#### インストール

## LSP

#### Python Language Server

> [Python Language Server - GitHub](https://github.com/palantir/python-language-server)

## ツール

### リンターツール

#### Pyflakes

#### McCabe

#### pycodestyle

#### pydocstyle

#### Flake8

#### Pylint

### 自動コード整形

#### isort

#### Black

フォーマット:

```bash
$ black <filename>
```

変更点を表示:

```bash
$ black --diff <filename>
```

フォーマット済みかチェック:

```bash
$ black --check <filename>
```

#### autopep8

フォーマット: 

```bash
$ autopep8 --in-place <filename>
```

コード整形のレベルを指定:

```bash
# `aggressive`オプションを複数付けることでレベルを指定する
$ autopep9 --in-place --aggressive --aggressive <filename>
```

変更点を表示:

```bash
$ autopep8 --diff <filename>
```

#### YAPF

`autopep8`よりも優れている？  

フォーマット:

```bash
$ yapf --in-place <filename>
```

変更点を表示:

```bash
$ yapf --diff <filename>
```

### 型検査

#### mypy

### 現在の使用ツール

```bash
$ pipenv install --dev flake8 pylint
$ pipenv install --dev --pre black
```

## 参考

> [もうPythonの細かい書き方で議論しない。blackで自動フォーマットしよう](https://blog.hirokiky.org/entry/2019/06/03/202745)  
> [2019年に向けてPythonのモダンな開発環境について考える](https://techblog.asahi-net.co.jp/entry/2018/11/19/103455)  
> [これで決まり！最強自動コード整形ツール3選！](https://www.kimoton.com/entry/20181223/1545540702)  
> [Pythonのスタイルガイドとそれを守るための各種Lint・解析ツール5種まとめ！](https://blog-ja.sideci.com/entry/python-lint-pickup-5tools)  
> [Pythonのコード改善のためのツール5つを試してみた](https://minus9d.hatenablog.com/entry/2018/10/22/235604)  
