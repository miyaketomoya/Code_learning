# リーダブルコードを読んで雑にメモしていく
## 第７章　制御フローを読みやすくする

- 条件式の書き方
  - 変化するものが左、右に比較対象の式<br>
    🙆‍♂️`if length > 10: # 左に定数`<br>
    🙅`if bytes_expected > bytes_received: # 基準となるものが右`
- if/else文のルール
  - 条件は否定系よりも肯定系
  - 単純な条件を先に書く
  - 関心を引く条件や目立つ条件を先に書く
- 三項間演算子について
  - `1 if a == 1 else 2`のように単純に1か2の2択であればわかりやすい
  - `(num << tmp) if a == 1 else (num << -tmp)` のように分岐後にさらに操作があると見にくい -> if/else文の方が良い

- do/while文は避ける
- 関数から早く出すのはok
- クリーンナップコードを使用する(with open~など)
- gotoは複雑になるので使わない
- **ネストを浅くする**
  - できることならif文のなかにif文などは避ける

## 第８章 巨大な式を分割する
- 説明変数を用いる<br>
  ```
  #before
  if line.split(":")[0].strip() == "root":

  #after -> 説明変数をおく
  username = line.split(":")[0].strip()
  if username == "root"
  ```
- 要約変数を用いる
  ```
  # before
  if request.user.id == document.owner_id:
    hogohoge
  if request.user.id != document.owner_id:
    hugahuga
  ```
  - 対して大きな式ではないが、コードが本当に言いたいことを考える
  - このコードが言いたいのは「ユーザは文章を所持しているか？」
  ```
  # after
  user_owns_document = (request.user.id == document.owner_id)
  if user_owns_document:
    hogehoge
  if !user_owns_document:
    hugahuga
  ```
- ドモルガンの法則で論理式を書き換える
- 「頭がいい」コードに気をつける(１行に落とし込めるのが偉いわけではない！)
  - `x = a || b || c `の演算子の効果を確認(TODO)
- より優雅な方法を見つける（反対を考えてみるなど）

## 9章 変数と読みやすさ
- 役に立たない一時変数
  ```
  # このnowはいるか？　複数は使われてないし、datetime.datetime.now()はぱっと見でも理解できるものでは？
  now = datetime.datetime.now()
  root_message.last_view_time = now
  ```
- タスクはできるだけ早く返す
  ```
  # before
  def remove_one(array, value_to_remove):
    index_to_remove = null
    for i in range(len(array)):
      if array[i] == value_to_remove:
        index_to_remove = i
        break

  if index_to_remove != null:
    # index_to_remove番目の値を削除
  ```
  - このコードでindex_to_removeは必要だったのか？
  ```
  # after -> 早めに返すことは悪くない。むしろいいこと
  def remove_one(array, value_to_remove):
    for i in range(len(array)):
      if array[i] == value_to_remove:
        # i番目の要素を削除
        return
  ```

- 宣言の位置と使用する位置ができるだけ飛ばないようにする
- **定数の位置を下げる**
  - 初めにたくさん定義あると、読んでいる人はこれから変数全てのことを考慮に入れないといけなくなる
- 一度だけ書き込む変数を使う
  - イミュータブルな変数で宣言すれば、読む人は安心して読み続けられる

## 第10章 ⭐ここから大事そう！！
    

