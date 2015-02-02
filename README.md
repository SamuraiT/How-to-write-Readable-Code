# How-to-write-Readable-Code
For all of you who are trying to write readable code

リーダブルコードを書きたいあなたへ

1. 表面的に奇麗にする
----------------------
```
プロジェクトに参加する時は書くよりも読む方が多い，多くのコードを読み少しの機能を追加する．
その時に，あなたのコードが醜いと悲惨なことになるだろう．
```

* 変数/関数名/クラス名/には情報量が多い名前にする．

`e.g password -> plaintext_password`これで，暗号化されていないパスワードと分かり，後で暗号化をしないままDBに突っ込むことはないだろう．

`e.g var start = (new Data()).getTime() -> var start_ms = ...`*start*の単位まで付ければ出力する時に単位ミスを起こさないだろう

* クラス, 関数，変数の書き方に区別をつける．

これは言語で依存するので，その言語・会社のコーディング規約を参照されたい（以下，pythonの例）
```
class-> class ClassName(object):
private member variable -> _member_variable

function-> def function_name():

variable -> variable_name
```




2. 
