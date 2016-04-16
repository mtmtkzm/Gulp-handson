sass.md

## もう一歩向上させるWEBデザイン

### Sample code
※ Sassの機能のサンプルコードであり、そのコード自体が適切な設計かどうかは不問です。

- 分からなければ、CSSをそのまま書いてもだいじょーぶ（＝完全上位互換）

```sass
.menu {
  background-color: #333;
}
.menu a {
  color: #fff;
}
```

- コメントアウトは、`/* コメントアウト */`以外に、`// コメントアウト` が使える

```sass
// 背景色を、暗めのグレーに指定
.menu {
	background-color: #333;
}
```

- ネスト（入れ子構造）ができる

```sass
.menu {
	background-color: #333;

	a {
		color: #000;
	}
}
```

- 変数が使える

```sass
$gray: #333;
$white: #fff;

.menu {
	background-color: $gray;

	a {
		color: $white;
	}
}
```

- いろんな値で四則演算ができる

```sass
$dark-gray: #444444;

.darkgray {
  color: $dark-gray;
}

.light-gray {
	color: $dark-gray * 2;
}
```

- コードを使いまわせる

```sass
@mixin border-radius {
	border: 5px solid #333;
	border-radius: 10px;
}

.boxA {
	@include border-radius;
}

.boxB {
	@include border-radius;
}
```

- プログラミング言語的な処理もできる（if分岐）
変数で `$theme: 1;` としてるので情熱的な赤いテーマになっている例。

```sass
$theme: 1;

@mixin theme {
	@if $theme == 0 {
		background-color: blue;
		color: yellow;
	}
	@else if $theme == 1 {
		background-color: red;
		color: orange;
	}
	@else {
		background-color: green;
		color: brown;
	}
}

.body {
  @include theme;
}
```


- プログラミング的な処理もできる（for文で繰り返し）

```sass
@for $i from 0 through 5 {
	.box_#{$i*30} {
		width: 30px * $i;
	}
}
```


- 便利な関数が用意されている

1. 16進数の色指定に対して透明度を指定できる

```sass
p {
	color: rgba(#666666, 0.5);
}
```

2. 中間色をつくれる

```sass
div {
	background-color: mix(#fff, red, 50%);
}
```

3. ちょっと明るく、ちょっと暗く

```sass
p {
	color: darken(#fff, 30%);
}
p {
	color: lighten(blue, 30%);
}
```

4. 四捨五入、切り上げ、切り捨て

```sass
$width: 100px;
.box {
	width: $width / 6;
}
.box-round {
	width: round($width / 6);
}
.box-ceil {
	width: ceil($width / 6);
}
.box-floor {
	width: floor($width / 6);
}
```
