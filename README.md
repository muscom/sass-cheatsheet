# Sass
## 変数 / Variables
### Sass
```Sass
$primary-color: #cccccc;

body {
  background-color: $primary-color;
}
```
### CSS
```CSS
body {
  background-color: #cccccc;
}
```
## 入れ子 / Nest
### Sass
```Sass
nav {
  ul {
    color: #ff0000;
  }

  li {
    font-size: 16px;
  }
}
```
### CSS
```CSS
nav ul {
  color: #ff0000;
}

nav li {
  font-size: 16px;
}
```
## ファイル分割 / Partial
ファイル名の先頭に _ を付ける
```Sass
_partial.scss
```
## 外部ファイルの読み込み / Import
### Sass
```Sass
@import '_partial/_partial'
```
### CSS
```CSS
.partial {
  font-size: 24px;
}
```
## @mixin
### Sass
```Sass
@mixin border-radius($radius) {
  -webkit-border-radius: $radius;
  -moz-border-radius: $radius;
  -ms-border-radius: $radius;
  border-radius: $radius;
}

blockquote {
  @include border-radius(10px);
}
```
### CSS
```CSS
blockquote {
  -webkit-border-radius: 10px;
  -moz-border-radius: 10px;
  -ms-border-radius: 10px;
  border-radius: 10px;
}
```
## @extend と継承
### Sass
```Sass
// 継承用のルールセット
%Block {
  border: 3px solid #000000;
  border-radius: 20px;
}

// 一度も使わないルールセットはCSSには出力されない
%NoneUsedBlock {
  border: 50px solid #ffffff;
  border-radius: 10px;
}

// @extend
.block {
  @extend %Block;
}

// border-colorを上書きする
.block-note {
  @extend %Block;
  border-color: #cccccc;
}
```
### CSS
```css
.block, .block-note {
  border: 3px solid #000000;
  border-radius: 20px;
}

.block-note {
  border-color: #cccccc;
}
```
## 演算子 / Operators
### Sass
```Sass
/* ** Operators ** */
.container {
  width: 100%;

  article {
    width: 600px / 960px * 100%;
  }

  aside {
    width: 360px / 960px * 100%;
  }
}
```
### CSS
```css
.container {
  width: 100%;
}

.container article {
  width: 62.5%;
}

.container aside {
  width: 37.5%;
}
```
## 配列 / Lists
```Sass
/* ** Lists ** */
// カンマ区切り
$comma-list: 10px, green, none;
// スペース区切り
$space-list: 10px green none;
```
## 配列の長さの参照
### Sass
```Sass
.sampleClass {
  /* $comma-listの長さ */
  $length-comma: length($comma-list);
  content: $length-comma;
  /* $space-listの長さ */
  $length-space: length($space-list);
  content: $length-space;
}
```
### CSS
```css
.sampleClass {
  /* $comma-listの長さ */
  content: 3;
  /* $space-listの長さ */
  content: 3;
}
```
## 配列のn番目の値の参照
### Sass
```Sass
.sampleClass {
  $nth: nth($comma-list, 3);
  content: $nth;
}
```
### CSS
```css
.sampleClass {
  content: none;
}
```
## 配列インデックスの参照
### Sass
```Sass
.sampleClass {
  $val-index: index($comma-list, green);
  content: $val-index;
}
```
### CSS
```CSS
.sampleClass {
  content: 2;
}
```
## 配列のn番目に新しい値をセットする
### Sass
```Sass
.sampleClass{
  /* 元のリスト */
  $current-list: $comma-list;
  content: $current-list;
  /* 2番目に新しい値をセット */
  $new-list: set-nth($comma-list, 2, blue);
  content: $new-list;
  /* 元のリストの値は変わらない */
  content: $current-list;
}
```
### CSS
```CSS
.sampleClass {
  /* 元のリスト */
  content: 10px, green, none;
  /* 2番目に新しい値をセット */
  content: 10px, blue, none;
  /* 元のリストの値は変わらない */
  content: 10px, green, none;
}
```
## 配列の結合
### Sass
```Sass
.sampleClass {
  /* セパレーターの指定無し */
  $joined-list: join($comma-list, $space-list);
  content: $joined-list;
  /* セパレーターにカンマを指定 */
  $comma-joined-list: join($comma-list, $space-list, comma);
  content: $comma-joined-list;
  /* セパレーターにスペースを指定 */
  $space-joined-list: join($comma-list, $space-list, space);
  content: $space-joined-list;
}
```
### CSS
```CSS
.sampleClass {
  /* セパレーターの指定無し */
  content: 10px, green, none, 10px, green, none;
  /* セパレーターにカンマを指定 */
  content: 10px, green, none, 10px, green, none;
  /* セパレーターにスペースを指定 */
  content: 10px green none 10px green none;
}
```
## 配列への値の追加
### Sass
```Sass
.sampleClass {
  $append-list: append($comma-list, append-value);
  content: $append-list;
}
```
### CSS
```CSS
.sampleClass {
  content: 10px, green, none, append-value;
}
```
## 配列の組み替え
### Sass
```Sass
// 組み替え用の配列
$size-list: 1px 2px 3px;
$color-list: blue green gray;
$style-list: solid dashed dotted;

// 配列を組み替え
.sampleClass {
  $zipped-list: zip(
    $size-list,
    $color-list,
    $style-list
  );
  content: $zipped-list;
  /* 配列を1つずつ抽出 */
  content: nth($zipped-list, 1);
  content: nth($zipped-list, 2);
  content: nth($zipped-list, 3);
}
```
### CSS
```CSS
.sampleClass {
  content: 1px blue solid, 2px green dashed, 3px gray dotted;
  /* 配列を1つずつ抽出 */
  content: 1px blue solid;
  content: 2px green dashed;
  content: 3px gray dotted;
}
```
