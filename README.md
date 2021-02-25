### jQuery「noConflict」を使って同一ページ内でバージョンの異なる複数のライブラリを組み込む方法
jQueryを組み込む場合、jQueryのバージョンに依存して動作しなかったりということがまれにあります。  
例えば、以下のようにjQuery1.4.4を読み込んでいるとします。  

```Javascript
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.4.4/jquery.min.js"></script>
<script src="jquery.sample.js"></script>
```

任意のプラグイン「jquery.sample.js」は1.4.4には対応しておらず、1.8以上のjQueryを必要とするため、上記のような順でライブラリを読み込むとエラーが発生します。  
  
ここで、1.4.4はCMSのテンプレートとして組み込まれており、サイト全体への影響なども踏まえて簡単にはバージョンアップはできません。  
本来、それらの影響を踏まえてバージョンアップすることが望ましいですが、「バージョンアップできない」という判断に至ったとします。
