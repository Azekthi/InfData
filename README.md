# InfData
ACEINF の計測データをまとめておくためのリポジトリです。

## ファイル フォーマット

```
# Comment
Column Name 1	Column Name 2	Column Name 3
Foo	0.5?	Bar,Baz
```

各行が一つのアイテムであり各列はタブ文字で区切られています。最初のアイテムは列名です。  
各列の意味についてはファイルに含まれるコメントをご参照ください。

値の末尾に `?` がある場合、その値が未確定であることを示します。  
未確定の値を使用した計算は実測と異なる結果となる場合があります。ご了承ください。

値が `,` で区切られて複数の値が入っていることがあります。

## 謝辞
このデータは多くの方のご協力がなければ成り立ちませんでした。  
[Berkut Method](http://berkut.blog.jp/) にて基となるデータを公開してくださったブログ主様、  
多くのデータの収集・計算に関してご協力いただいた月見リナ様、  
およびゲーム内の実測値を提供していただいた多くの皆様にこの場を借りて感謝を申し上げます。

## ライセンス
[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")](http://creativecommons.org/publicdomain/zero/1.0/deed.ja)  
InfData に含まれるファイルは CC0 でライセンスされています。  
どなたでも自由にご利用いただけます。

## 連絡先
mfakane <<star@sorairo.pictures>>
