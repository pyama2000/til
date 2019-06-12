# パスワードハッシュ関数: Scrypt, Bcrypt, ARGON2

パスワードを安全に保存する方法はMD5やSHA1, SHA256, PBKDF2, Bcrypt, Scrypt, Argon2などのハッシュ関数を用いた方法や平文で保存する方法がある。  
しかし、平文で保存することは論外として, MD5やSHA1, SHA256はパスワードを保存する方法としては適していない。  
その点では、Scrypt, Bcrypt, Argon2はパスワードを保存するのに適している。  

## ハッシュ関数の特徴

### PBKDF2

PBKDF2は以前からあり古いものではないが、GPU上での並列化やFPGAを使ったパスワード解析では簡単に解析される。

### Bcrypt

BcryptはPBKDF2よりもGPUやFPGAなどを使ったパスワード解析に対して耐性はあるがオフラインでの解析に対しては弱い部分がある。

### Scrypt

Scryptは良いパスワードハッシュ関数で、BCryptよりも優れている。

### Argon2

Argon2はPHC(Password Hashing Competition)で優勝したパスワードハッシュ関数。  
現在最も良い選択肢である。

## Argon2

Argon2にはArgon2iとArgon2dの2つのバージョンが存在していて、Argon2iはサイドチャネル攻撃に対して有効なもので、Argon2dはGPUを使ったパスワード解析に対して有効なものである。  

## 参考

> (Password Hashing: Scrypt, Bcrypt and ARGON2)[https://medium.com/@mpreziuso/password-hashing-pbkdf2-scrypt-bcrypt-and-argon2-e25aaf41598e]
