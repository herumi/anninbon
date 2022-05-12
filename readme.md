# 『暗認本』補足

[『暗認本』紹介ページに戻る](https://herumi.github.io/anninbon/)

## sec.06 安全性
Q. アルゴリズムは曖昧性のないように書くべきとあるのに「十分大きなnに対してほぼ～」という表現があいまいで分からない。

A. 本では省略していますが数学的には厳密な定式化をします。
気持ち的にはたとえば「ほぼ2倍」というのが2倍からどれぐらいずれているかをεで表します（ε=0.1とか0.0000001とか）。
そして誤差がεよりも小さくなるようなNを求めます（Nはεに依存しうる）。
εをどれだけ小さくしてもn > Nなら常に誤差がεより小さくなるようなNを見つけられる状態を「十分大きなn」と表現しています。

## sec.07 暗号技術の危殆化

>p.054 「大きなデータを手元の小さい鍵で暗号化してサーバに置いておくという形で未来永劫安全という方法は現時点で存在しません。」

参考文献 : ["Communication Theory of Secrecy Systems", Shannon](http://netlab.cs.ucla.edu/wiki/files/shannon1949.pdf)

- perfect secrecy ; 暗号文から元の平文の情報を何も得られないこと。
- perfect secrecyを満たす共通鍵暗号は、秘密鍵のとり得る数が平文のとり得る数以上でなくてはならない。

## sec.10 乱数
`/dev/urandom`がIntelの乱数生成命令rdrandがハックされた場合に制御できる問題がLinux Kernel 3.8.13に存在した例。
- [@DefuseSec](https://twitter.com/DefuseSec/status/408975222163795969)

## sec.29 署名

>p.172 「（署名鍵）sは認証器の内部に安全に保存する。」

署名鍵の保存方法にはいくつか方法があります。

1. 本で紹介しているように認証器の内部に安全に保存する。
1. もう一つは署名鍵sをその認証器だけが復号できる方法で暗号化してRPに保存してもらう方法です。
この方法だと認証器に保存する必要がないのでストレージの容量が少なくて済みます。
ただし、認証時にRPから認証器にその情報を送ってもらって復号する必要があります。

「[6.2.2. Credential Storage Modality](https://www.w3.org/TR/webauthn-3/#sctn-credential-storage-modality)」参照

## sec.31 タイムスタンプ

- ハッシュ値を連鎖させるリンクトークン方式はブロックチェーンの肝ですが、タイムスタンプの規格としては世界的に使われない傾向にあります。
  - NTTデータのSecureSealは2020年に終了しました。
- 現在は時刻認証局のTSA証明書を使ったPKI方式が主流です。
- [総務省のタイムスタンプについて](https://www.soumu.go.jp/main_sosiki/joho_tsusin/top/ninshou-law/timestamp.html)
  - 2021年7月、[日本データ通信協会](https://www.dekyo.or.jp/)が日本のタイムスタンプサービスの指定調査機関として[時刻認定業務の受け付け開始](https://www.dekyo.or.jp/tb/data/top/20210730.pdf)しました。
- PKI方式のタイムスタンプは通常10年保証されます。そしてタイムスタンプがついたデータやそれを検証する認証局の公開鍵証明書などをまとめて別のタイムスタンプをつけること（アーカイブタイムスタンプ）でより長い有効期間を得られます。
  - [第10回 電子認証、タイムスタンプ、そして長期署名－後編－](https://www.otsuka-shokai.co.jp/erpnavi/topics/column/digital-evidence/chokishomei2.html)
