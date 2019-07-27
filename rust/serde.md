# `serde`を使用する上で

`serde`の`Deserialzie`と`Serialize`を使う上で2つの方法がある:  

- `serde_derive`をインポート
- `derive`featureを追加

これからは`derive`featureを使うほうがいいと思う。

## `serde_derive`をインポートする方法

Cargo.toml:
```toml:Cargo.toml
[dependencies]
serde = "1.0"
serde_derive = "1.0"
```

main.rs:
```rust: main.rs
use serde::{Deserialize, Serialize};
use serde_derive::{Deserialize, Serialize};

#[derive(Deserialize, Serialize)]
pub struct Foo {}
```

## `derive`featureを使う方法

Cargo.toml:
```toml:Cargo.toml
[dependencies]
serde = { version = "1.0", features = ["derive"] }
```

main.rs:
```rust:main.rs
use serde::{Deserialize, Serialize};

#[derive(Deserialize, Serialize)]
pub struct Foo {}
```

## 参考文献

> [serdeの `derive` feature と名前空間の困った関係](https://qiita.com/qnighy/items/74ff6436860c79ceb940)
