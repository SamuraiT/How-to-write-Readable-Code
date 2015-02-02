# How-to-write-Readable-Code
For all of you who are trying to write readable code

リーダブルコードを書きたいあなたへ．
*注意*：これはリーダブルコードを私なりにまとめたものである．

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
```python
class-> class ClassName(object):
private member variable -> _member_variable

function-> def function_name():

variable -> variable_name
```




2. 誤解されるような名前をつけるな
-------------
* 限界値を条件判断するような場合

体重が`100kg`より重ければエレベータに乗れないとしよう．
そうしたら，あなたは`TOO_MUCH_WEIGHT = 100`とするかもしれない．

```python
TOO_MUCH_WEIGHT = 100
if your_weight > TOO_MUCH_WEIGHT:
      Raise OverWeightError():
```
だが，この変数名だと`TOO_MUCH_WEIGHT`を含めるのかわからない．本来ならば100kgを超えないようにとしたい．
その場合は変数名に`max`を付けよう
```python
MAX_WEIGHT_KG = 100
if your_weight > MAX_WEIGHT_KG:
      Raise OverWeightError():
```
ついでに単位も付けた．

* pythonの配列の用に最初は含めて，最後は含めない時は`begin`, `end`を使う
* 両方含めるときは，`first`, `last`を使う
* ブール値には`is, has, can, should`を使う．ただし，`scheme, ruby`では`eql?`のように`?`が使われている
* get, sizeという名前のメソッドには軽量(`O(1)`)なメソッドが期待されている．

3. コメントについて
-------------
コメントで自分が名前を付けた変数に補足しようとする人がいる．
それはやめて，情報量のある明確な変数名にして，コメントをなくそう．

```python
意味不な変数名

car = 1000000 #車の値段
```

```python
car_price = 1000000
```

変数は他の場所で使われる事の方が多い．どんなに定義した場所で補っても使われる時は意味不明なのである．
その変数名/関数名を補うような名前を付けるならちゃんと変数名を考えるべきである．



たまに分かりきったコメントをする人がいる．
```python
#分かりきったコメント
def calc_average(nums):
      """
      numsの平均を計算して，平均を返す
      """
      ....
```
これは関数名を見れば分かる．
そうではなくて，もっと重要なこと，思った事を書こう
```python
def calc_average(nums):
      """
      calc_averageはO((length of nums)^2)かかる．
      だから長い配列を渡すとやべー時間がかかる．
      """
      ....
```
こっちの方がかなりましだが，もっと詳細にもかける．(`注意:普通に計算すれば平気の計算にO(len(nums)^2)はかかりません`)
```python
def calc_average(nums):
      """
      FIXME: calc_averageは`O((length of nums)^2) = O(n^2)`かかる．（実装が難しい）
      長い配列を渡すと一定時間かかるので注意．
      TODO: 計算量をO(n)にする
      """
      ....
```
こうすれば，問題があり，あとで直すべき関数であるとわかる．

#### コメントを書くに当たってすべきこと

1. 実装した上で考えている事をとりあえず書く
2. コメントを読んで修正箇所を見つける
3. 修正する

