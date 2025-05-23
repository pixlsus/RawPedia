---
title: White Balance jp
contributors:
  - Yz2house
---

<div class="pagetitle">

ホワイトバランス

</div>

## イントロダクション

　一般的に、デジタル画像は3原色、レッド、グリーン、ブルーの混合で構成されています。様々な情報源からその理由を詳しく知ることも出来ますが、如何なる現像プログラムにおいても、撮影した画像を再現する前に、色々な方法でこれら3原色の値を補正することが最初のステップです。その補正方法の一つがホワイトバランスを基本にするもので、撮影された画像の中のニュートラルな色（ホワイト）が引き続きニュートラルに映るようにすることです。本来ニュートラルな色（ホワイト、グレー）であるべき部分の映りで、ホワイトバランスが正しいかどうか簡単に判別出来ますが、ホワイトバランスの補正は全ての色に影響します。

　ホワイトバランスの補正は、適切な色を得るまで、3原色の値に異なる数を掛け合わせることで行います。この調整を簡単に行うために、直接的に3つの乗数を操作するのではなく、ブルー-イエローの軸に沿って色を補正する色温度スライダーとマゼンタ‐グリーンの軸に沿って色を補正する色偏差スライダーを使います。

　ニュートラルカラーとは、3原色、レッド、グリーン、ブルーの値が同じである色のことです。例えば、R=G=B=65%とR=G=B=90%の色はどちらもニュートラルカラーです。但し、前者は後者より暗くなります。画像の中のニュートラルカラーであるべきスポットが正しいかどうかは、各RGB値が同じである、L\*a\*b\*色空間のa\*値とb\*値が同じである、或いはヒストグラムのRGBインディケーターバーがお互いに重なりあっていることで、確認出来ます。たとえ貴方のモニターのキャリブレーションが誤っていても同じように確認できます。色の変化に対する人間の目の知覚機能は、周りの色やそれを見る部屋の明るさにも影響されます。見た目の色は信用しないことです。前述した方法で確かめることが肝要です。

　ホワイトバランスが誤っていると、画像に色被りが生じます、典型的には画像の印象が暖か味が強過ぎたり（オレンジ）、冷た過ぎたり（ブルー）します。ユーザーの中には、それを独創的な効果として使う人もいますが、RawTherapeeに備わった機能や作用には、ホワイトバランスが適正であることを前提にしたものが数多くあります、例えば[露光補正の](Exposure/jp.md)中のハイライト復元機能や、[詳細レベルによるコントラスト調整の](Contrast_by_Detail_Levels/jp.md)肌色の目標/保護、[ウェーブレット](Wavelets/jp.md)
の青空の色相-トーン、
[CIE色の見えモデル02/16などです](CIECAM02/jp.md)。従って、独自の色味を作り出すためにホワイトバランス機能を使うことは奨められません。この機能あくまでニュートラルな色をニュートラルに見せるための調整に使うもので、独創的な色味を加える場合は、[カラートーン調整](Color_Toning/jp.md)、或いは他の機能を使うべきでしょう。

　ホワイトバランス機能はオン・オフすることが出来ます。オフにすると、raw画像の編集時に3原色に対する乗数が、それぞれR=1、G=1、B=1、となります。色の診断やUniWBイメージを扱う時に役立つでしょう。

## インターフェイスの説明

### 方法

- [image:Wb-camera.png](image:Wb-camera.png.md) カメラ
    
  カメラにプログラムされているホワイトバランスを使う方法です。raw画像だけ（JPEG画像は同時に撮らない）撮影する場合は、カメラのホワイトバランスを自動に設定する方が、一般的に良い結果が得られるようです。

<!-- -->

- [image:Wb-auto.png](image:Wb-auto.png.md) 自動
  - RGBグレーを使った自動調整
      
    自動的にホワイトバランスを設定する選択で、撮影シーンの平均色がニュートラルグレーであることを前提にしています。幅広い撮影シーンに対応しており、その後の手動による画像調整を行う起点としては良いかもしれません。
  - 色温度の相関関係を使った自動調整
      
    　通常、“RGBグレーを使った自動調整”よりカラーバランスがいいでしょう。このアルゴリズムは、画像の色と429個の参照スペクトルカラー配列の間の最適な相関関係（スチューデントのt検定）をベースにしています。

    - 　但し、このアルゴリズムは誤った結果になることがあります：
      - 　演色評価数（CRI）が100から離れている光源、例えば“水中”や“蛍光灯”、“Led”などの下で撮影した画像には適しません。
      - 　DNGコンバーターや他のコンバーターを使ってDNG形式に変換したファイルの一部では悪い結果になることがあります。
      - 　撮影条件が極端な場合（輝度が非常に低い、など）に結果が悪くなります。
    - 　インターフェイスに相関関係の値（t検定の結果）を表示します：
      - 　1000が表示された場合は、反復計算が行われず、前の結果が使われていることを意味します。5002が表示された場合は、アルゴリズムによる計算が失敗したことを意味します。
      - 　0.01より低い値が表示されれば、調整結果が良いことを意味します。
    - 　⟨自動ホワイトバランス　色温度のバイアス⟩で、算出結果を微調整できます。
    - 　このアルゴリズム（Itcwb）の解説は[別項にあります](White_Balance/jp#色温度の相関関係アルゴリズム.md)。

<!-- -->

- [image:Wb-custom.png](image:Wb-custom.png.md) カスタム
    
  2つのスライダーで色温度と色偏差を設定するか、スポットホワイトバランス機能を使うか、或いはその両方を使って貴方ご自身で設定する方法です。

<!-- -->

- 光源によってプリセットされたホワイトバランス
  - [image:Wb-sun.png](image:Wb-sun.png.md) 昼光（晴天）
  - [image:Wb-cloudy.png](image:Wb-cloudy.png.md) 曇天
  - [image:Wb-shade.png](image:Wb-shade.png.md) 日陰
  - [image:Wb-water.png](image:Wb-water.png.md) 水中
  - [image:Wb-tungsten.png](image:Wb-tungsten.png.md)
    タングステンライト
  - [image:Wb-fluorescent.png](image:Wb-fluorescent.png.md)
    蛍光灯
  - [image:Wb-lamp.png](image:Wb-lamp.png.md) ランプ
  - [image:Wb-led.png](image:Wb-led.png.md) LED
  - [image:Wb-flash.png](image:Wb-flash.png.md) フラッシュ

### ピック

<figure>
<img src="White_balance_1_before.png"
title="White_balance_1_before.png" />
<figcaption>White_balance_1_before.png</figcaption>
</figure>

<figure>
<img src="White_balance_1_after.png"
title="White_balance_1_after.png" />
<figcaption>White_balance_1_after.png</figcaption>
</figure>

　ピックのボタン
![<File:Color-picker.png>](Color-picker.png "File:Color-picker.png")をクリックすると、画面上を動くカーソルがスポイトのアイコンに変わります。このスポイトを画面のニュートラルカラーの部分でクリックして、画像全体の正しいホワイトバランスを決めます。

　グレー或いはホワイトのニュートラルトーンのスポットをピックしますが、そのRGBいずれかの色チャンネルがクリップしているスポットは補正に適しません。クリッピングしている色チャンネルからは、色情報が得られないからです。ホワイトバランスで言うところの、この“ホワイト”は、R=100％、G=100%、B=100％ではありません、これではクリップしているからです。代わりにグレーな影、たとえそれが非常に明るくとも、クリップしていないのであれば、そこを選びます。また、黒い所も避けます。黒い部分では色情報が不足しているのでホワイトバランスの算出が正確に出来ません。

　的確なホワイトバランスを見つけるため、画像の異なる部分で何回でもピックすることが出来ます。スポイトのサイズを変えるのは、ドロップダウンボックスで行います。

　この機能は拡大画面でも使えます。右クリックで機能をキャンセルすると、スポイトが通常のカーソルに戻ります。

### 色温度と色偏差

　色温度スライダーはブルー-イエローの軸に沿って色を変えるスライダーです。左に動かすと画像の印象が冷たく（ブルーが増す）、右に動かすと暖かく
（イエローが増す）なります。

　色偏差のスライダーはマゼンターグリーンの軸に沿って色を変えるスライダーです。左に動かすと、画像にマゼンタの色味が増
し、右に動かすとグリーンの色味が増します。

### ブルー/レッドイコライザ

　レッドとブルーの比率を増やしたり減らしたりすることで、通常の“ホワイトバランス”の性質を変えます。通常の光環境と大きく異なる条件で撮影した場合、例えば水中、或いは入力プロファイルのカラーマトリクスが不適切なため、通常のキャリブレーションでは十分に補正が出来ない場合に使えます。

### 自動ホワイトバランスの色温度バイアス

　自動ホワイトバランスの色温度バイアスのスライダーで自動的に算出された色温度を任意にずらします。自動的に算出される色温度の印象を変える（ウォーム、或いはクール）ことが出来ます。

## ホワイトバランスと露出の関係

　ホワイトバランスは色温度と色偏差で表現されますが、raw画像の編集が行われる際には、重みを付けたレッド、グリーン、ブルーチャンネル置き換えられます。これらの重みは、rawチャンネルが作業色空間で（通常、ProPhoto
RGB）飽和に達した時に、最も重みの少ない色チャンネルが飽和するように調整されています。言い換えると、露光量補正0.0、ハイライト復元オプションが無効の時、可視範囲全体がrawの裏付けにより完全に定義出来ると言うことです。ホワイトバランスの調整によりこれら重みが変わるので、大幅な調整を行うと露出が若干変わるかもしれません。

## 色温度の相関関係アルゴリズム

　以下、このアルゴリズムの原理と実装に関する技術的な解説をしますが、これらの理解がなければ機能が使えないということではありません。あくまで技術的な側面に興味のある方々のための記述です。このホワイトバランスの補正を使うには、カラータブのホワイトバランス→"方式"→"自動"→"色温度の相関関係"と進みます。

　以下、このアルゴリズムは"Itcwb"（Iterative Temperature Correlation
White Balance） という略称で引用します。

　多くのホワイトバランスアルゴリズムはグレートーンをベースにしていますが、Itcwbはそれらとは異なり色をベースにしています。簡単に言うと、アルゴリズムが画像の中の多数の色を、一連の基準色とその関連スペクトルデータと比較/分析し、補正します。

### アルゴリズムの端緒

　このアルゴリズムはJacques
Desmisによって開発されました。非公式論文の概要を読んで閃いたそうです。アルゴリズムは3段階のステップに分けられます：

- 　a) xyY値の比較
- 　b) スペクトルデータの分析
- 　c) カラーヒストグラムの分析

　これら3段階が以下に説明するアルゴリズムのベースになっています。ゼロから開発したアルゴリズムなので、既存のアルゴリズムも、そのコードもありません。

### パフォーマンス

　Itcwbの働きの良し悪しは以下の要因に影響を受けます：

- 　画像からサンプル抽出した色と、主調色（肌色、空の色、花の色など）の選択
- 　計算の基礎に使われる一定のパラメータ。例えば、撮影時のカメラのホワイトバランス、レッドとブルーに作用する色温度とマゼンタとグリーンに作用する色偏差、など。
- 　RGBチャンネル乗数の選択と光源の色温度に基づいた計算
- 正確な計算式（行列式）と5ナノメータのスペクトルデータを使った、基準色のXY値の計算。\[観測された色\]=\[光源\]\*\[物体色\]/\[標準観測者10°\]（或いは、オプションまたは環境設定で観測者を２°に変更）
- 　グリーン/マゼンタとレッド/ブルーのバランスを均等に考慮した複数回の繰り返し計算。
- 　撮影時の光源が、昼光光源（色温度：4100Kから12000K）や黒体放射光源（2000Kから4100K）で、その演色評価指数（CRI）が100に近いかどうか
- 　スチューデントのt検定を使った統計的相関関係

### 参照スペクトルチャート

　429個の参照スペクトルカラーの出所と特質：

- 　ウェブサイトから見つけた葉や花の色のデータ
- 　カラーチェッカー24、或いは他のカラーチャートから得たデータ
- 　数年前にキャリブレーションのために開発した468色のチャートからのデータ
- 　Colorlab（Logo Gmbh）のユティリティのデータ
- 　これらの色がカラーパレット全体に渡ってほぼ均一に配分されます。
- 　また、これらの色はニュートラル、或いはグレーに近い、少し彩度がある、パステルカラー、彩度が高いという順で並べられます。
- 　色の比較分析はクロマ要素で行われるため、輝度の強さはさほど重要ではありません。

### 原理全般

- 　デモザイク処理後に、水平、垂直の２方向で、3ピクセルごとに1ピクセル選びレッド、グリーン、ブルーのRGB値の表を作成します。ピクセル値は0～65535の範囲に収まるように調整します。精度を上げるためにこの設定を変更することも出来ます。
- 　次に、2つの自動ホワイトバランス調整に共通するアルゴリズム"自動"、による処理を行います。RGBチャンネル乗数を計算し、それらを"Itcwb"或いは"RGBグレー"に送ります。
- 　"自動"がItcwbに送るパラメータには、重要である色温度の値（カメラのExifデータ）と、0.77～1.30の範囲の色偏差の値（カメラのExifデータ）が含まれます。色偏差に関しては、この範囲を超える昼光光源と黒体放射光源は存在しないので、範囲外の数値が送られれば、その計算結果は誤りとなります。

### 単純化した色温度の相関関係アルゴリズム

　2段階からなるアルゴリズムです。

1.  ステップ1
    1.  　2000K～12000Kの範囲にある各温度と色偏差に対してRGB乗数を計算します。
    2.  　各色温度に対して429個のスペクトルデータからXY値を計算します。
    3.  　基準色と比較する色温度のデータ範囲を選択します。
    4.  　ヒストグラム形式でxy値を計算し、各色温度で最も一般的に使われる可能性のある色（肌色、空の色など）を236色の中から選択します。
    5.  　これらデータを数値の昇順に並べます。
    6.  　最も頻繁に表れるデータで、画像の色度を計算します。
    7.  　429個のカラー配列から基準色を選択するために、色度のΔEを使います。
    8.  　基準となる色温度に応じて基準色のRGB値を計算します。
2.  ステップ2
    1.  　色温度と色偏差に応じて、選択した各基準色のXY値を計算します。
    2.  　RGB乗数を使ったxy値から画像のRGB値を計算します。
    3.  　t検定の最初の計算を行います。
    4.  　各色温度と色偏差の範囲で、一致するスペクトルデータからカラーチャンネルの乗数とXY値を計算します。
    5.  　グリーン（色偏差）に応じて、相関係数を計算します。
    6.  　計算結果を並べ替えます。
    7.  　正しい色温度と色偏差を決定するための最適化を図ります。
    8.  　これらパラメータを〈自動〉に戻します。
    9.  　結果を表示し、Improccoordinator.ccを更新します。

#### 最近（2023年5月）行った改良

- 　このアルゴリズムは始動の前に基準値を決めておく必要があり、デフォルトではカメラのデータ（色温度と色偏差）をその基準値として使うようにしています。しかし、幾つかのケースで、それでは結果が誤りになることがありました。カメラの色偏差が1.5より大きい時、色温度が3300Kより低い、或いは7700Kより大きい時に起こっています。そこで、その場合は、新しい基準値として"自動RGBグレー"で計算された値を使います（或いは、カメラのデータと自動RGBグレーの計算値をミックスした値）。
- 　カメラの色温度が、4000Kより低い、或いは6000Kより高い場合は、2工程のアルゴリズムで処理が実行され、十分に標準値から離れた別な値がより適切な結果を生むかどうか確認します。カメラの色温度が4000Kから6000Kの間にある場合は、カメラのデータとの差が小さい値を使った、別のアルゴリズムによる処理が実行されます。
- "ローサンプリング＆カメラの設定を使わない"オプションを有効にすると、アルゴリズムの作用において、システムはカメラと"
  自動RGBグレー"の値をミックスして使います。
- 　色偏差の計算を改良しました。
- 画像の色分析（ホワイトポイントからの乖離）から、パッチの最適化を図っています。理論的には、値が低いほど結果が信頼できることになります。
- 　画像データのヒストグラムを生成する前に、若干ノイズ除去（3x３　メディアン）を適用しています。
- 　ヒストグラムのデータを計算する際に、外れ値を除くために色域抑制を適用します。

#### インターフェイスに表示されるデータ　レンダリングの限界

- 　インターフェイスに表示されるr、g、b：RGBのチャンネル乗数は、情報としての表示であり、変更することは出来ません；
- 　相関係数：画像データとスペクトルデータの間に相関関係がどれ程あるか示します。しかし、あくまで目安です。何故なら、元々比較的不確定である（どのデータを使う？その範囲は？最初の色温度/色偏差の選択で最良の妥協点を求めますが、最初のデータを使うのが最善なのか？）パッチを、"適切である"と仮定しているからです。
- 　処理工程（1、或いは２）と色温度の変更：実行されているアルゴリズムの工程と変更可能な色温度を表示します。"2工程処理"が選択されていると、"2工程処理のアルゴリズムを除外する"というオプションが使えますが、他の場合はこのオプションは使えません。
- 　色の読み込み：画像から読み込む色の数です（"サンプリング"に応じて）。最大は237色でCIExyダイヤグラム全体をカバーします。
- 　色のパッチ：パッチの最適化を図るための指標です。"最良の"均一領域（空や肌など）と及び詳細を持つ領域を考慮するために、指数法則に基づいた重みを付けます。
- 　サイズ：画像から一度に選択する色の数を指します（該当するピクセル最大値から最小値まで）。
- 　パッチのΔE：画像データとスペクトルデータ間のパッチのΔEを表示します。
- 　データ x
  9：各色に関し、記録された数の最大値と最小値を表示します。絶対最小値は任意で400に設定しました。実際の評価をするために、これらの値を9で乗じています。処理時間を短縮するために3ピクセルごとに1ピクセル（水平と垂直方向）だけを解析しているからです。

##### レンダリングの限界

　Itcwbは複雑なアルゴリズムですが人間ではないので、処理する画像が人物写真なのか、風景写真なのか、データの構造やパターンがどうであるかの判断は出来ません。従って、前述のパラメータを使ってシステムを制御する際には多くの注意が必要です。確かに殆どの場合、これらパラメータは信頼に足るものですが、例外も少なくありません：

- 　例えば、"色のパッチ"のサイズが小さいから適切であるとは限りません。この指標は"色温度/色偏差"の組み合わせが最適であるかどうかの指標になりますが、小さいことがベストでないケースもあり、その場合は、パッチのサイズを変えてみます。
- 　"ΔE"が最低値を示したから最適であるとは限りません。確かに、この値は基準値に近い色温度/色偏差に換算したもので、乖離が小さいことを示していますが、それがユーザーにとって最良の結果であるとは限りません。
- 　"相関関係係数"が最も低いからといって最適な結果であるとは限りません。この指標は参考色に近い色の色温度と"色相"との最適化を示すものですが、やはりユーザーにとってそれが最良の結果であるとは言い切れません。

　このシステムはアルゴリズムを働かせる前に、どの基準値（カメラのホワイトバランス、或いはグレースケールのホワイトバランス）を使うかを決定します。次に、アルゴリズムの工程１だけを使うか、工程２も使うかを決定します。アルゴリズムによる最初のステップは、各工程に関するパッチの最適化を"色のパッチ"を使って行います。次に、色温度と色偏差の範囲のテストが行われ、パッチのΔEと相関関係が計算されます。ΔEと相関関係の最小乗数値を考慮することで妥協点を見出します。一方、撮影時の光源がカラーマトリクスを決定しているD65（Adoveが取り入れている）から大きく乖離している場合は、データの読み取りとそれらの解釈が不完全となる確率が増えるため、表示される結果が正しくない場合もあります。しかし、たとえ不完全になる確率が増えても、標準A光源のカラーマトリクスの計算とその入力も、それなりに重要です。

　処理が上手くできない画像もあるでしょう。例えば、画像の中に強い色（レッドやイエロー、パープルなど）が１つ或いは２しかなく、実質的にホワイト（グレー）な部分が無い画像は最適化の処理が上手く行かないと思います。また、光源が昼光とは大きく異なるもの、例えばLEDの場合、或いは複数の光源下で撮影された画像なども処理が不正確になる可能性があります。

### 自動ホワイトバランス　色温度のバイアス

　⟨自動ホワイトバランス　色温度のバイアス⟩は、ホワイトバランス補正の結果を簡単に微調整する機能です。

　実際には、最初の色温度を変えて、色温度、色偏差、相関の再計算を行います。その目的は：

- 　測色の再調整。色の見えモデルの色順応と少し似ていますが、同じものではありません。
- 　色ずれを起こさずに、ユーザーが期待していた色映りに近づける。

### ユーザーによる手動設定

　このアルゴリズムで使うパラメータの変更はgithubの開発ブランチ、[`whitebalanceopt`](https://github.com/Beep6581/RawTherapee/pull/6643)で行います。

　殆どの画像に対し、デフォルトの設定で十分と思われますが、アルゴリズムを実行する上で独自の変更を行う余地を残しています。

　カラータブのホワイトバランスでは、アルゴリズムに適用する一連の設定を表示していますが、将来的にはこれら設定の多く（出来れば全て）を削除したいと思います。これら設定の削除も基本的にはアルゴリズムの改良につながります。

　これら追加的設定を表示するためには、環境設定→カラーマネジメント→ホワイトバランスと進み、その中の色温度の相関の自動設定で、該当するボックスにチェックを入れます。ホワイトバランスで、"色温度の相関"が選択されていない場合は、機能表示がグレーアウトになります。

#### 関連パラメータ

　影響のあるパラメータ（先験的）：

- 　3x３のマトリクス
  - 　3x３のマトリクスはデモザイク後のrawデータを有効なデータに変換するためのマトリクスのことです。この画像処理に必要不可欠なマトリクスは、RawTherapeeのrawに関わる幾つかのアルゴリズムでも使われています。元々、Adobe©に由来するもので、Dcraw或いはAdobe
    DNG
    Converter（タグ付けされたマトリクス）から得られたものです。しかし、Adobe自身はどうやってこのマトリクスを手に入れたのでしょう？社内の研究から？それともカメラメーカーとの連携？一つ言えるのは、これらマトリクスは共通したプロセスで作られていると考えられることです。同じ場面、同じ光源、同じ撮影条件（シャッタースピード、絞り、レンズなど）で撮影が行われ、一般的なrawの処理が行われれば、有効なカラーデータ（輝度やダイナミックレンジではなく）は概ね同じになるはずです。ここではベイヤー配列のセンサーで撮影されたデータのことを述べていますが、他のタイプのセンサーも存在します。明らかに異なる特性を持っており、特に非ベイヤー配列は光学系が異なるだけでなく、特定のデモザイクアルゴリズムが必要です。しかし、マトリクスの違いによるItcwbの結果の差は小さいはずです。　
  - 　このマトリクスは光源がD65の場合に適しています。Exifの中には標準A光源（タングステン光）に適しした別のマトリクスもあります。テストを行った結果、色温度2600Kで撮影された画像では、標準A光源用のマトリクスを使う方の結果が多少良いと感じられました。しかし、RawTherapeeが出来ることはカラーマトリクスの処理だけであり、どのマトリクスを使うかを選択させるために、何百台のカメラ情報を集めることは現実的ではありません。このカラーマトリクスはItcwbに影響を及ぼします。
- 　各撮像センサーが持つ特性：
  - 　ダイナミックレンジ：古い型のカメラではその多くのダイナミックレンジが12Evですが、最近のカメラであれば15から16Evになります。しかし、ダイナミックレンジがItcwbや輝度の構成に及ぼす影響は小さいので無視できます（色域を決定する以外は）。
  - 　ホワイトレベルとブラックレベル：rawデータの全体的処理にとっては非常に重要なパラメータですが、余程外れた設定をしない限りItcwbへの影響はないはずです。
  - 　センサーの色域：色の転写には限界がある、と言うような公式見解は聞いたことがありません。変換マトリクスを適用する前であれば、Prophotoの色域を十分に上回っているのでItcwbに与える影響はあるとしても非常に小さなものです（つまり、結果は変わりません）。
- 　色の種類と強さ：xyY色度座標上の色の位置のことで、画像の色がホワイトポイントに近い（パステルカラー或いはニュートラルカラー）のか、又は人間の知覚の限界に近い色なのかを座標で示します。
- 　各原色、レッド/グリーン/ブルーに関係するこれらの色の分布。
- 　このアルゴリズムは、可視領域全体をカバーする"xy"空間を236個の領域に分割し、画像の色の分布がどの様な状況であるかを考慮します。例えば、多くの色調がホワイトポイント（ニュートラル）に近いとか、主調色（空の色や肌色）に近いとか、などです。
- 　光源：例えば、日が当たっている部分と影の部分の両方がある画像は、実質的に2つの昼光光源（日に当たっている部分の色温度は5000Kに近く、影の部分は7000Kに近い）の下で撮影された画像ということになるので、理論上、単一のホワイトバランス（色温度と色偏差）で補正することは難しいということになります。光源が蛍光灯やLEDであれば更に複雑です。しかし、これは何もItcwbに限った問題ではなく、あらゆるホワイトバランスアルゴリズムに共通するものです。ローカル編集タブの⟨自然な彩度とウォーム/クール⟩のウォーム/クール機能は、この2重光源（日と影のある画像）の補正に非常に役立ちます。
- 　光源に関する問題は他にもあります。光源には色温度とスペクトルデータをつなげる理論的な定義がありますが、これらの公式は完璧ではありません。また、あらゆる環境；緯度、海抜、撮影日時、気象条件（霧など）が、色偏差に影響を与えます（つまり、1.0から外れる）。
- 　標準観測者2°と標準観測者10°：後者の方が人間の視覚特性に近いものです。
- 　ここで、XYZデータで知覚される色は、3つのマトリクスの組み合わせであることを思い出して下さい：
  - 　光源のスペクトルデータ（色温度と光源の性質の作用）
  - 　参照色のスペクトルデータ（分光器で計測）
  - 　標準観測者（2°又は10°）のスペクトルデータ

　原則、このアルゴリズムは画像処理上（非常に複雑）の欠点を補正するようには設計されていません。将来的にはそれら問題を克服できるかもしれませんが、今の目的ではありません。

#### 各種設定

- 　CIExyダイヤグラムと色域：以下に2つのダイヤグラム（上は輝度Lが10、下は輝度Lが50）を示していますが、CIExyダイヤグラムに含まれている色でも、色域の中には入らない色があることが分かります。

<figure>
<img src="Gamu-comp10.jpg" title="Gamu-comp10.jpg" />
<figcaption>Gamu-comp10.jpg</figcaption>
</figure>

<figure>
<img src="Gamu-comp50.jpg" title="Gamu-comp50.jpg" />
<figcaption>Gamu-comp50.jpg</figcaption>
</figure>

<figure>
<img src="Rec2020_Pointer.jpg" title="Rec2020_Pointer.jpg" />
<figcaption>Rec2020_Pointer.jpg</figcaption>
</figure>

<figure>
<img src="sRGB2jdcmax.jpg" title="sRGB2jdcmax.jpg" />
<figcaption>sRGB2jdcmax.jpg</figcaption>
</figure>

　数週間にわたるユーザーによるテストとアルゴリズムの最適化を図ったことで、ユーザーが3つのパラメータを直接調整することが出来るようにしました：

　手動による設定

- 　色偏差の微調整：アルゴリズムを始動する際に、基準となる"色偏差"を調整することが出来ます。機能的には"自動ホワイトバランス　色温度のバイアス"とほぼ同じものです。調整値を使ってアルゴリズムが計算をやり直します。場合によっては、アルゴリズムを誘導するために、"2工程アルゴリズムを除外"オプションを有効にする必要があるかもしれません。
- 　
  "2工程アルゴリズムを除外"：これは背後で複雑な処理を管理するオプションです。アルゴリズムにより選択された工程が１つの場合は、このオプションが有効でも無効でも関係ありませんが、２つの工程が選択された場合はこのオプションを使って、どちらかの工程に変えることが出来ます。注意：色温度が標準A（タングステン光　2855K）に近い画像で、２つの工程の一方だけが選択された場合は、カラーマトリクスに関連したエラーで結果が誤ってしまう場合があるので、表示された指標（相関関係のΔEなど）には注意が必要です。
- 　 画像データのサンプル抽出：4つの選択肢があります。
  - 　ローサンプリング：これは色のデータをsRGBの範囲に制限した中からのサンプリングです。特定の条件の下では（カメラが設定した色偏差が0.8より大きい場合）、アルゴリズムがカメラの設定値を使わないようにします。
  - 　ミディアムサンプリング（デフォルト）：レーザーポインターの色域に近いデータからのサンプリングで、ベータRGBの原色が使われます。従って、減法混色における人間の視覚に近い色域を得られます。ベータEGBより若干広いRec2020を使うことも可能です。
  - 　カメラのXYZマトリクス：カラーマトリクス（Adove）から直接的に導いたマトリクスの範囲からのサンプリングです。
  - 　完全なCIEダイヤグラムに近い色データ：JDCmaxの最大限度、つまり完全なCIEダイヤグラムに近い色データからのサンプリングです。
  - 　これら4つのサンプリングは"作業プロファイル"とは関係がなく、ホワイトバランスの補正以外の処理にも影響はありません。
  - 　スペクトルデータが十分である限りは、４つ目の選択肢を使うことが望ましいと思います。たとえ、そのために想像上の色（imaginary
    color）が発生した（主にグリーンにおいて）としても、"作業プロファイル"を適用する前の連続性が保たれるからです。但し、例外となるケースが２つあります：１）画像がスペクトルデータの参照値にないデータを含んでいる（非常に稀だと思われます）。この場合、ΔEと相関関係が偏ります。２）色域の広い画像において、結果が損なわれるので、意図的に一部のデータを考慮に入れたくない、つまりカメラのデータを使いたくない場合です。
  - 　カラータブの⟨カラーマネジメント⟩で、"入力プロファイルなし"、或いは"カメラの標準的プロファイル"を選択していると、サンプリングのための基準データが、その後に使用されるデータと同様に処理されてしまうことに注意して下さい。

　pp3での設定：

- 　Itcwb_rgreen：色偏差のスチューデント検定を検知します。スチューデント検定値と色偏差値（昼光/黒体放射光源の場合は1に近い）の間の最適な妥協点を見つけるための繰り返し回数のことです。2回から5回までの選択ができますが、3回が最も妥協点を得られると思われるので、デフォルトでは3回が設定されています。
- 　Itcwb_nopurple=false：デフォルトではこの設定をしていません。輝度の復元が必要な画像では、このオプションを有効にする必要があるかもしれません。
- 　Itcwb_minsize：最小パッチサイズを設定するものです。デフォルトは20に設定されています。
- 　Itcwb‐色偏差の幅：繰り返しの中で検査する色偏差の値の幅を設定します。最低幅は0.82から1.25、最大幅は0.4から4です。
- 　Itcwb_delta：色偏差の繰り返しテスト中の色温度のΔ。各色偏差のテストでは固定されています。色温度の差は考慮されます。

　"オプション"ファイルの中で設定できるもの

- Itcwb‐Δスペック：Verboseを"true"にすると、ΔEの偏差が設定されている値より大きい場合、その画像データとスペクトルデータをコンソール上に表示します。デフォルトの設定値は0.075です。
- Itcwb‐最大サイズ：最大のパッチサイズを指定します。デフォルトでは70に設定されています。

#### 色順応

　Itcwbアルゴリズムによる演算結果は客観的な数学の基礎に基づいた計算の妥当性を示しています。但し、この結果は他のホワイトバランス調整機能同様、人間の知覚特性を考慮していません。周囲の光環境や同時対比による影響のほか、特に、色温度の違い（物体を見る光源が、測色の基準であるD50と異なる場合）に対する視覚/脳の順応特性が考慮されていません。この乖離を埋めるために、2018年に筆者は、ホワイトバランス機能に色順応機能を"統合"することを提唱しましたが、現在は⟨色の見え＆明るさ⟩の中の色順応機能を使ってユーザー自身が補正を行うようにしています。

　それを行うためには⟨色の見え＆明るさ⟩の設定‐プリセットの中のモードを"自動シンメトリック"に変更します。そうすると、2つの色順応が適用されるようになります。一つは"場面条件"の基準となる光源（通常はD50ですが、変更も可能です）に対する色順応、もう一つは"観視条件"の基準となる光源に対する色順応です。デフォルトではこれら色順応適用を90％にしてありますが、適用率は変更出来ます。また、画像の映りに暖かみや冷たさを加えるために、"観視条件"の色温度を変更できます。その他、色の明るさ＆見えの設定である、"絶対輝度"や"周囲環境"を変えることも出来ます。詳しくは当該項目の解説を参考にして下さい。

### Itcwbによるホワイトバランス調整の例

　例1：
[トルコのソルトマウンテン](https://drive.google.com/file/d/1azCxu1midw6dcuN7SbvbAiJH4pxX5BTA/view?usp=sharing)
(`_ASC4145.NEF` CC BY-SA 4.0 Jacques Desmis)

　一見、問題が無さそうなそうな画像ですが、写真という点では補正が難しい画像です。理由は：

- 　ソルトマウンテンのホワイト部分は処理が難しい画像です。このアルゴリズムは全般的に処理の難しい複雑な構造に影響を受けます。
- 　この画像の補正ポイントはホワイトバランスと色の配分ですが、画像の大部分を占める、空、木々、山の色はsRGB色空間に収まっていますが、下部の花の色（レッド、オレンジ、イエロー）はsRGBの範囲から大きく離れています。これらをどの様に扱うのか、設定による影響を考慮する必要があります。

　例2：[食堂](https://drive.google.com/file/d/1MMNzw3tPQuMeD5baqDlBXRvl4lDy2mLX/view?usp=sharing)
(`LunchingRoom.CR2` CC BY-SA 4.0 Rawtherapee)

　この画像に対しては、アルゴリズムが複雑な状況を上手く補正します。

- 　カメラが設定するホワイトバランス（デフォルト）では、著しい色被り（グリーン）が発生しています。
- 　そこで、ホワイトバランスの⟨方式⟩を"自動"の"RGBグレー"、或いは"色温度の相関関係"を適用することで適切に補正されます。

　例3：[ロンドン橋](https://drive.google.com/file/d/1CiQ2t4KyD3tdCiNNhskqUG2cH9LT2ly7/view?usp=sharing)
(`london_bridge_moving_1.pef` CC BY-SA 4.0 Maciej Dworak)

　この画像にはItcwbと色順応機能の両方を使う必要があります。

- 　デフォルトのカメラのホワイトバランスを使うと、グリーン/イエローの色被りが生じます。
- 　Itcwbを使うことで、数学的に適当な妥協点が得られますが、結果として得られる色温度が高く、その分、色が過剰に暖かみを帯びます（人物の顔や、デッキのロープにそれが見られます）。
- 　⟨色の見え＆明るさ⟩を自動シンメトリックモードにして補正します。

　例4：[キャリブレーションテスト用のパターン](https://drive.google.com/file/d/1YFeoPL-RhStftDCCkbDNlmj8New_SgX0/view?usp=share_link)
(`DSCF5334.RAF` CC BY-SA 4.0 RawTherapee)

- 　この画像を使ってテストを試みた理由は2つあります：一つはこの画像のraw形式がRAF、つまり撮像センサーがベイヤー配列ではないカメラで撮影された画像であること。二つ目の理由は、画像がほぼ純粋なホワイトとブラックを含んでいること（画像の主調色がグレーであるため、アルゴリズムが影響を受ける可能性がある）。
- 　情報量の多い画像で、表示デバイスがキャリブレーションされていないようですが、結果は現実（ホワイトとブラック、カラーチェッカー）に近いと感じられます。
- 　もちろん、アルゴリズムがこの画像をキャリブレーションテスト用のパターンであると認識するわけでなないので、幾つかのオプションを試しました。色域の限界に近い色が含まれているので、"CIEダイヤグラムを強制的に使う"を有効/無効の両方で、"色の順番に並べる"を有効/無効の両方で、"パーフルを使用しない"を無効にする、で試しましたが、どれもカメラの設定を使った画像と大きな違いはありませんでした。

　例5：[逆光](https://drive.google.com/file/d/1iqpj-vT3dqUmaXKOQE7QB_rynf4cbRPC/view?usp=share_link)
(`DSC02973.ARW` CC BY-SA 4.0 Jacques Desmis)

- 　この画像は筆者がカリブ海を旅行した時に古いSonyのカメラで撮影したものです。
- 　カメラのホワイトバランスと、Itcwbとでテストしてみました。

　例6：[インペイント‐オポーズドを適用した画像](https://drive.google.com/file/d/1ZxucMREXAAFlBijiBiBZoH9kG4-O2GYb/view?usp=share_link)
(`Nikon - D800 - 14bit uncompressed (3_2).NEF` CC0 1.0 Pascal Obry)

- 　"インペイント‐オポーズド"（ハイライト復元の方式の一つ）を適用した画像に対する影響、特に色偏差、を知るためにこの画像を選びました。
- 　カメラのホワイトバランスを使った画像に"インペイント‐オポーズド"を適用すると、空の部分に大きなアーティファクトが発生しました。
- 　Itcwbを使いホワイトバランスを補正し、色々な調整をしてみました。

### Itcwbを含むバージョン5.9含まないバージョン5.9との互換性

　Itcwbアルゴリズムが導入されているバージョン5.9と、Itcwbが入っていないバージョン5.9ではその互換性に制限があります：

- 　XYZ色空間で使われる標準観測者は10°だけで、2°は使えない。

　旧5.9バージョンでItcwbが使われている画像のpp3が読み込まれると、"色温度の相関関係"が表示されますが、表示される関連情報は、ホワイトバランスの乗数、色温度と色偏差、標準観測者2°の代わりに10°の観測者だけです。
