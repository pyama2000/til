# `git checkout`の使い方

- コンフリクト解消
- ブランチ切り替え

## コンフリクトが起きたときにHEADとマージブランチのどちらかに一発で`checkout`

### `git checkout --ours` / `git checkout --theirs`

```bash
# マージ先のブランチ(HEAD)を反映したい場合
$ git checkout --ours <file>

# マージブランチを反映したい場合
$ git checkout --theirs <file>
```

> (git rebase競合時、git checkout --theirsとか--oursする時には注意が必要)[https://qiita.com/genreh/items/c058077cdb5f78a851fa]
