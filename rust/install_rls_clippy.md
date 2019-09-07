# RLSとClippyをnightlyチャンネルでインストールするときの注意点

nightlyチャンネルは毎日変更があるため、RLSとClippyをビルドできない日がある。  
nighylyチャンネルをインストール・アップデートする場合は[rustup-components-history](https://rust-lang.github.io/rustup-components-history/)でどの日がビルドできたかを確認してその日のツールチェツールチェーンをインストールしなくてはならない。

```bash
$ rustup install nightly-2019-09-05
$ rustup component add rls clippy rustfmt --toolchain nightly-2019-09-05

# プロジェクトにインストールしたnightlyバージョンを適用する
$ rustup override nightly-2019-09-05
```
