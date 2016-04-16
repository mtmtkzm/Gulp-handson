gulp.md

## まずは何より、Gulpを使う準備
ここから様々な場面で、黒い画面が出てきますが、
Gulpを習得するついでに黒い画面に対する抵抗感を拭い去りましょう！

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
まずは該当フォルダに移動
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
`gulpfile.js`というファイルを作成（中身は空でok！）

## 実際に、Gulpタスクを組んでいこう
