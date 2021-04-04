# Night-Light-Compe

## Reference
|No.|Title|
|---|----|
|1|[宇宙教育教材「JAXA オリジナル Google Earth Engine Apps 集](https://edu.jaxa.jp/news/2020/i-0315.html)|
|2|[低所得国における夜間光と社会・経済指標の相関関係](https://dept.sophia.ac.jp/econ/econ_cms/wp-content/uploads/2016/11/62-2.pdf)|
|3|[条件付き生成アドバーサリア・ネットワークを用いた中解像度衛星画像のセマンティック・セグメンテーション](https://arxiv.org/pdf/2012.03093.pdf)|

## Notebook
|No.|Content|
|---|----|
|nb001|EDA|
|nb002|EDA|
|nb003|夜間光データから土地価格を予測ベースモデル(by cha_kabu)|
|nb004|夜間光コンペ Baseline(xgb,lgb,cat)(by tubo)|
|nb005|「夜間光データから土地価格を予測」のLSTMベースライン(by daikiclimate)|
|nb006|夜間光データから土地価格を予測 BaseLine(by mst8823)|
|nb007|base blockにまとめる|

## TO DO
 - yearの影響が出やすい地域とそうでない地域の分類
 - areaが狭くても地価が高い土地も、低い土地も混在してるから区別できる特徴量が作れば強い？
  - SumLgihtとareaを順位つけてみる？areaが狭くてSumLgihtが大きいのは栄えているはず
  - これをtarget encoudingしてみてはどう？
 - TabNet
 - LSTM
 - StratifiedGroupKfoldとGroupKFold
 - nb004のモデルで、LGBMRegressorとかと比べて精度の差は？
 - カーネルPCA
 - pivottableはfillna(0)しとくのがよいかも？
 - スタッキングの参考になりそう[url](https://github.com/nyk510/atmacup10/blob/master/src/exp__027.py)
 - 紙幣の価値みたいなのだせないかな？20年もあったら物価とかいろいろ影響してない？
 - モデル作るときはyearが全部そろってるやつだけか、関係なく全部集計どっちがよい？

## LOG
### 20210320
### nb003
 　- CV:0.598351
 　- LB:0.554372
 - gitの使い方を間違えreadme消えた...はあ...
 - histplotって対数変換してくれるんだ
 - SumLightとMeanLightで面積分かりそう
 - MeanLightのmaxは63以上がないからめっちゃ多くなる
 - PlaceIDは均等に分布しているからランダムに割り当てられている（←規則性があれば首都圏付近で塊りができそう)
 - MeanLightがでかいほど地価も高いっぽい。というのも63付近は顕著だが、それ以外は傾向がなさそう
 - SumLight低くて地価高いのはやっぱ都会か？
 - areaが狭くても地価が高い土地も、低い土地も混在してるから区別できる特徴量が作れば強い？
 - PlaceIDリークしないように注意な
 - MeanLightが63とるのは毎年ではないかもしれないから特徴量へ

### 20210321
### nb003続き
 - aggメソッド便利
 - 間に挿入する文字列'.join(\[連結したい文字列のリスト\])
 - ### nb004
 - goupbyオブジェクトはreset_index()でDataFrameに戻る
 - StratifiedGroupKfoldとGroupKFoldどっちがよいのだ

### 20210322
### nb004続き
 - LGBMRegressorとかCatBoostRegressorじゃないけど何が違うんだ？
  - パラメータでregression指定すれば結局いっしょなのかな？
 - docker-composeでgpu有効にしていなかった。でもどうやってやるのだ・・・

### 20210328
### nb004続き
  - CV:0.593936
  - LB:0.769067
 - 結局dockerでgpu有効にできませんでした！！！！つまり進捗0です！！！！ubuntuにするか～
### nb005
   - CV:0.5286
 　- LB:0.564726
 - LSTMのベースライン
  - LSTMとは：ニューラルネットワークの１種.
  - LSTM(Long Short Term Memory)は「忘却する・入力する・出力する」という３つのゲートで成り立っている
 - round(f,1):fを小数点第一位まで丸める
 - StandardScaler()するときは、trainにfit_transformして、testにはfitをせずtransformだけなのはなんでだったっけ・・・？何かで見た気がする
 - PlaceIDのカウントが22だったら1992～2013までのデータが全部ある。全部そろってないのはそぎ落とすといいのか？
 - pytorch何してんのかわかんねえな・・・

### 20210329
### nb006
 - callable:呼び出し可能であるかを判定
 - 結局shiftは何が目的で使ってるんだ？
 - pivot_table使ってるところ可視化できないかな
 - pcaの使い方？

### 20210331
### nb006続き
 - dockerでgpuが認識されないのはワイだけじゃなかった・・・まますさんもだった・・・
 - コンペ終わったらやってみよう
 - 学習データとテストデータに同じPlaceIDがないためPCAによる次元削減することで分散表現チックに特徴量を得ることができるかもしれない

### 20210401
### nb006続き
  - CV:0.5341
  - LB:0.491471
 - returnの代わりにyield出てきた
 - seedを何個か使って平均とっているの初めて見たな

### 20210402
### nb007
 - map関数に渡すときDataFrameで渡しててエラーになった。Seriesで渡さないといけない

### 20210403
### nb007続き
 - diffとかってlagって言い変えたりしてる
 - listにSeriesっぽい配列入ってたら、pd.concatでDataFrame化できるのね

### 20210404
### nb007続き
  - CV:0.54312
　- LB:0.606241
 - キメラnotebookできた
 - そしてLB低いな・・・
### nb008
  - CV:0.54467
  - LB:
 - キメラnotebookできた
 - lagとshiftをrange(0,22)→range(-20,22)にしてみたがCV下がった・・・
### nb009
  - CV:0.54468
 - 特徴量にランク入れてみた
### nb010
  - CV:0.54467
 - pivotするときにNanは0にしてみる
 - CVに変化なし
### nb011
  - CV:0.54097
 - aggでskewなくした
 - diff,shiftのrangeを0からにしてたから1からに
 - param変更
### nb012
  - CV:0.54259(bin=100)
  - CV:0.542833(bin=300)
  - CV:0.54250(bin=500)
  - CV:0.54297(Area:bin=500, SumLight:bin=1000)
  - CV:0.54296(Area:bin=50, SumLight:bin=100)
  - CV:0.54275(Area:bin=90, SumLight:bin=700)
 - binning追加

### 20210405

 - target encorfingとGroupKFoldのrandom_stateを一致させような
 - PlaceIDでpcaの対象増やしたいな
 - 単体モデル
