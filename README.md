## jQuery「noConflict」を使って同一ページ内でバージョンの異なる複数のライブラリを組み込む方法
jQueryを組み込む場合、jQueryのバージョンに依存して動作しなかったりということがまれにあります。  
例えば、以下のようにjQuery1.4.4を読み込んでいるとします。  

```Javascript
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"></script>
<script src="jquery.sample.js"></script>
```

任意のプラグイン「jquery.sample.js」は1.4.4には対応しておらず、1.8以上のjQueryを必要とするため、上記のような順でライブラリを読み込むとエラーが発生します。  
  
ここで、1.4.4はCMSのテンプレートとして組み込まれており、サイト全体への影響なども踏まえて簡単にはバージョンアップはできません。  
本来、それらの影響を踏まえてバージョンアップすることが望ましいですが、「バージョンアップできない」という判断に至ったとします。

### 一度jQueryを無効にして新しいものを読み込む
この問題の解決策の1つとして、一旦jQueryを無効にする方法があります。

```Javascript
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"></script>
<script type="text/javascript">
	$.noConflict();
</script>
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>
<script src="jquery.sample.js"></script>
```

ライブラリの衝突を回避する「noConflict」を実行することで、jQueryの省略文字「$」が解放されます。  
その後に、別のjQueryを読み込むことで、結果的に部分的にバージョンアップされたことになります。  
  
つまり、「noConflict」より前のスクリプトは1.4.4で、後のスクリプトは1.8.2で実行されるわけです。

### 2つのjQueryを共存させる
「noConflict」の引数をtrueとし、オブジェクトに代入すると2つのjQueryを共存させることも可能です。  
  
  ```Javascript
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"></script>
<script type="text/javascript">
	$144 = $.noConflict(true);
</script>
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.2/jquery.min.js"></script>

<script type="text/javascript">
	$144('#sample').append('これはjQuery 1.4.4です');
	$('#sample').append('これはjQuery 1.8.2です');
</script>
```
このように、「$144」はjQuery 1.4.4として、「$」はjQuery 1.8.2として実行されます。
