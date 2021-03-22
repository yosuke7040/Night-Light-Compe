# Night-Light-Compe

## Reference
|No.|Title|
|---|----|
|1|[宇宙教育教材「JAXA オリジナル Google Earth Engine Apps 集](https://edu.jaxa.jp/news/2020/i-0315.html)|
|2|[低所得国における夜間光と社会・経済指標の相関関係](https://dept.sophia.ac.jp/econ/econ_cms/wp-content/uploads/2016/11/62-2.pdf)|

## TO DO
 - yearの影響が出やすい地域とそうでない地域の分類
 - areaが狭くても地価が高い土地も、低い土地も混在してるから区別できる特徴量が作れば強い？
  - MeanLightとareaをbinningで順位つけてみる？areaが狭くてMeanLight(SumLgiht)が大きいのは栄えているはず
  - これをtarget encoudingしてみてはどう？
 - TabNet
 - LSTM
 - StratifiedGroupKfoldとGroupKFold
 - nb004のモデルで、LGBMRegressorとかと比べて精度の差は？

## LOG
### 20210320
 - ### nb003
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
 - ### nb003続き
 - aggメソッド便利
 - 間に挿入する文字列'.join(\[連結したい文字列のリスト\])
 - ### nb004
 - goupbyオブジェクトはreset_index()でDataFrameに戻る
 - StratifiedGroupKfoldとGroupKFoldどっちがよいのだ

### 20210322
 - ### nb004続き
 - LGBMRegressorとかCatBoostRegressorじゃないけど何が違うんだ？
  - パラメータでregression指定すれば結局いっしょなのかな？
 - docker-composeでgpu有効にしていなかった。でもどうやってやるのだ・・・
