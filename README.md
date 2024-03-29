# 複数の画像群からJavaScriptでランダムに1つを選んで表示する方法
複数の画像リストの中から、JavaScriptでランダムに1つが選ばれて表示される仕組みを作ってみましょう。お気に入りの写真の中から1枚だけを毎回ランダムに選んで大きく表示させたい場合などに活用できます。

アクセスするたびに1枚がランダムに選ばれるだけなので、スライドショーで画像を順番に表示する場合とは異なり、大きなスクリプトを読み込んだり書いたりする必要はありません。リアルタイムに切り替わっていくわけではないので、ブラウザ上の表示はうるさくなりません。乱数を使って表示対象を選ぶだけの短いJavaScriptソースで作れます。ぜひ試してみて下さい。

## JavaScriptで画像を毎回ランダムに切り替える手順
複数の画像ファイル群からランダムに1枚を選んで表示させるには、JavaScriptを使えば簡単です。表示候補の画像ファイルリストを事前に用意しておき、乱数を使って1つを選び出して表示させるようになります。

必要なJavaScriptの処理は、下記の3点です。

1. 表示候補の画像ファイルを配列に登録
1. アクセスされるたびに乱数を使って1枚を選ぶ
1. 選んだ画像1つだけをサイト上に表示

## ソース

~~~javascript
<script type="text/javascript">
   var imglist = new Array(
      "flowerA.jpg",
      "flowerB.jpg",
      "flowerC.gif",
      "flowerD.gif" );
   var selectnum = Math.floor(Math.random() * imglist.length);
   var output = "<img src=" + imglist[selectnum] + ">";
   document.write(output);
</script>
~~~

上記を画像を表示させたい場所に記述します。

### var output = の規則について
上記のソースの場合、`<img src="https://imgcp.aacdn.jp/img-a/800/auto/aa/gm/article/2/3/8/0/5/flowerA.jpg">`と出力されてしまう。

imgにclassやidなどを付与したい場合は、下記のようにしなければならない。

~~~javascript
<script type="text/javascript">
var imglist = new Array(
"https://www.olp.co.jp/jobsite_assets/img/sigotora/loading1.png",
"https://www.olp.co.jp/jobsite_assets/img/sigotora/loading2.png",
"https://www.olp.co.jp/jobsite_assets/img/sigotora/loading3.png",
"https://www.olp.co.jp/jobsite_assets/img/sigotora/loading4.png" );
var selectnum = Math.floor(Math.random() * imglist.length);
var idtxt = "mitarashi";
var classtxt = "korokoro";
var widthtxt = "300";
var output = '<img src=' + imglist[selectnum] + '\tid="' + idtxt + '"\tclass="' + classtxt + '"\twidth="' + widthtxt + '">';
document.write(output);
</script>
~~~

出力html  
`<img src="https://www.olp.co.jp/jobsite_assets/img/sigotora/loading1.png" id="mitarashi" class="korokoro" width="300">`


* `var output`では、''(シングルクォーテーション)もしくは""(ダブルクォーテーション)でくくらなければならない。今回は出力内に""で囲う箇所がいくつかあったので、シングルクォーテーションから使い始める必要があるので、注意。
* `\t`はスペースの代わり。
* `idtxt`、`classtxt`、`widthtxt` は代入値。
