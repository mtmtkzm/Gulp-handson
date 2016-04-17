gulp.md

## まずは最初の作業環境
こんな感じでささっと作っちゃってください！
```
/project
  ┗ /src
     ┣ style.scss
     ┗ index.html
```

## Gulpを使う準備
ここから様々な場面で、黒い画面が出てきますが、
Gulpを習得するついでに黒い画面に対する抵抗感も拭い去りましょう！

### Node.jsのインストール
公式サイトにアクセス
https://nodejs.org/

### gulpのインストール

```
npm install -g gulp
```
OSXの環境でエラーが出た場合は、`sudo npm install -g gulp`で実行しなおしましょーう。

### package.jsonの作成
プロジェクトフォルダにpackage.jsonを作成します。
まずはプロジェクトフォルダに移動
```
cd path/to/project  <-- 自分のプロジェクトフォルダに移動
```

package.jsonを作成するコマンドを実行
```
npm init
```
確認ダイアログがいくつか出てくるが、Enterキーを連打でok！
（生成されるpackage.jsonを触ることで後から変更できます）

### gulpfile.jsの作成
`gulpfile.js`というファイルを作成し、そこに、
```js
var gulp = require('gulp');
```
とだけ記述しておきましょう。これはGulpを使うよ！っていう宣言。

## 実際にsassのGulpでコンパイルしてみる
### gulp-sassプラグインをインストール
```
npm install gulp-sass --save-dev
```

### タスクの内容をgulpfile.jsに追記
```js
// 今インストールしたgulp-sassを使います
var sass = require('gulp-sass');

// 'sass'っていうタスクを宣言し、処理を記述
gulp.task('sass', function() {
	gulp.src(['./src/style.scss'])    // 対象とするファイルを指定
		.pipe(sass())                // sassをcssにコンパイルする処理
		.pipe(gulp.dest('./public')) // 処理後のファイルを吐き出す場所を指定
});
```

しっかり保存。

### style.scssになんか書く
```scss
$gray: #333;
$red: #f00;

p {
	color: $gray;

	span {
		color: $red;
	}
}
```

### 実際にコンパイルしてみる
プロジェクトフォルダで、以下を実行。
```
gulp sass
```

そうすると、プロジェクトフォルダの中身が、こうなってるはずー
```
/node_modules
gulpfile.js
package.json
/project
  ┣ /src
  ┣  ┣ style.scss
  ┣  ┗ index.html
  ┗ /public
     ┗ style.css
```

### アウトプットスタイルを変更
style.cssを開くと、cssが見慣れない変な形になってると思います。
sassタスクにオプションを追加していつもの見た目にしてみましょう。
```
.pipe(sass({outputStyle: 'expanded'}))
```

## cssと同じように、index.htmlもpublicにコピーしたい
### コピータスクを作ろう
以下をgulpfile.jsに追記。
これがGulpオリジナルの機能なので、プラグインのインストールは不要。
```js
gulp.task('copy', function() {
	gulp.src('./src/index.html').pipe(gulp.dest('./public'));
});
```

### コマンド実行
```
gulp copy
```

こうなってればok！
```
/node_modules
gulpfile.js
package.json
/project
  ┣ /src
  ┣  ┣ style.scss
  ┣  ┗ index.html
  ┗ /public
     ┣ style.css
     ┗ index.html
```

## index.htmlを編集してstyle.cssを反映させよう
```
<link rel="stylesheet" href="style.css">
```
をindex.htmlに追記するだけですね。
ここで注意したいのが、  
編集・追加・削除等すべての作業をsrcフォルダ以下で行うこと。public以下は触らないようにする。

## 各タスクをwatch（＝変更監視）しよう
## src, publicそれぞれの対象ファイルの指定を変更
## ブラウザ自動リロードと、ローカルサーバの立ち上げをしよう
## 同期処理
