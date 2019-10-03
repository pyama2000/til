# `git submodule`の使い方

`git submodule`は外部のリポジトリを自分のリポジトリのサブディレクトリとして登録して、特定のcommitを参照する仕組みのことです。

## リポジトリ内に外部のリポジトリを追加する

| リポジトリ名 | 役割 |
|:-------------|:-----|
| module\_a    | 現在作業をしているリポジトリ |
| module\_b    | サブモジュールとして追加するリポジトリ |

```bash
# モジュールBを`submodule`という名前で追加する
$ git submodule add https://github.com/pyama2000/module_b.git submodule

# サブモジュールを追加した時点でcommitするとよい
$ git commit -m "Add XXX as a submodule"
```

> [Git submodule の基礎](https://github.com/pyama2000/til/blob/master/git_github/checkout.md)
