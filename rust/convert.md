# 型変換のTips

## Vec<String> -> Vec<&str>

`Vec<String>`を`Vec<&str>`に変換するときに普通にやると`Vec<&String>`になってしまう。  
以下のようにやると`Vec<&str>`に変換できる。


```rust
fn convert1(strings: Vec<String>) -> Vec<&str> {
    strings
        .iter()
        .map(String::as_ref)
        .collect()
}

fn convert2(strings: Vec<String>) -> Vec<&str> {
    string
        .iter()
        .map(|x| &**x)
        .collect()
}
```
