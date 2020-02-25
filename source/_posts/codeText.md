---
title: codeText
date: 2020-02-23 13:43:49
tags:
---

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    b{
      color:#c00;
    }
  </style>
  <script>
    function(){
      alert(123);
    }
  </script>
</head>
<body>
  <div id="abc"></div>
  <p class="abc" id="p" data-a="数据">p标签</p>
</body>
</html>
```
```css
sub,
sup {
  font-size: 75%;
  line-height: 0;
  position: relative;
  vertical-align: baseline;
}

sub {
  bottom: -0.25em;
}

sup {
  top: -0.5em;
}
```
```less
  @media screen and (device-aspect-ratio: 1280/720) { … }
  @media screen and (device-aspect-ratio: 2560/1440) { … }

  html:lang(fr-be)

  tr:nth-child(2n+1) /* represents every odd row of an HTML table */

  img:nth-of-type(2n+1) { float: right; }
  img:nth-of-type(2n) { float: left; }

  body > h2:not(:first-of-type):not(:last-of-type)

  html|*:not(:link):not(:visited)
  *|*:not(:hover)
  p::first-line { text-transform: uppercase }

  @namespace foo url(http://www.example.com);
  foo|h1 { color: blue }  /* first rule */

  span[hello="Ocean"][goodbye="Land"]

  E[foo]{
    padding:65px;
  }

```
```scss
/* Some example SCSS */

@import "compass/css3";
$variable: #333;

$blue: #3bbfce;
$margin: 16px;

.content-navigation {
  #nested {
    background-color: black;
  }
  border-color: $blue;
  color:
    darken($blue, 9%);
}

.border {
  padding: $margin / 2;
  margin: $margin / 2;
  border-color: $blue;
}

@mixin table-base {
  th {
    text-align: center;
    font-weight: bold;
  }
  td, th {padding: 2px}
}

table.hl {
  margin: 2em 0;
  td.ln {
    text-align: right;
  }
}

li {
  font: {
    family: serif;
    weight: bold;
    size: 1.2em;
  }
}

@mixin left($dist) {
  float: left;
  margin-left: $dist;
}

#data {
  @include left(10px);
  @include table-base;
}

.source {
  @include flow-into(target);
  border: 10px solid green;
  margin: 20px;
  width: 200px; }

.new-container {
  @include flow-from(target);
  border: 10px solid red;
  margin: 20px;
  width: 200px; }

body {
  margin: 0;
  padding: 3em 6em;
  font-family: tahoma, arial, sans-serif;
  color: #000;
}

@mixin yellow() {
  background: yellow;
}

.big {
  font-size: 14px;
}

.nested {
  @include border-radius(3px);
  @extend .big;
  p {
    background: whitesmoke;
    a {
      color: red;
    }
  }
}

#navigation a {
  font-weight: bold;
  text-decoration: none !important;
}

h1 {
  font-size: 2.5em;
}

h2 {
  font-size: 1.7em;
}

h1:before, h2:before {
  content: "::";
}

code {
  font-family: courier, monospace;
  font-size: 80%;
  color: #418A8A;
}
```


```vue
  <template>
    <div>

    </div>
  </template>

  <script>
    export default {

    }
  </script>

  <style lang="scss" scoped>
    b{
      color:#c00;
      a{
        color:#0c0
      }
    }
  </style>
```
```xml
<html style="color: green">
  <!-- this is a comment -->
  <head>
    <title>HTML Example</title>

  </head>
  <body>
    The indentation tries to be <em>somewhat &quot;do what
    I mean&quot;</em>... but might not match your style.
  </body>
</html>
```

```javascript
  setTimeout(()=>{
    console.log(123)
  });
  function(){
    alert(123);
  }
    var abc;
```
```js
  setTimeout(()=>{
    console.log(123)
  });
  function(){
    alert(123);
  }
    var abc;
```
```vue
<template>
  <div class="sass">Im am a {{mustache-like}} template</div>
</template>

<script lang="coffee">
  module.exports =
    props: ['one', 'two', 'three']
</script>

<style lang="sass">
.sass
  font-size: 18px
</style>
```

```php
<?php
$a = array('a' => 1, 'b' => 2, 3 => 'c');

echo "$a[a] ${a[3] /* } comment */} {$a[b]} \$a[a]";

function hello($who) {
	return "Hello $who!";
}
?>
```
```json
a:{
  a: 10,
  b: 30
}
```

```TypeScript
class Site {
   name():void {
      console.log("Runoob")
   }
}
var obj = new Site();
obj.name();
```
