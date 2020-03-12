---
title: sass
date: 2017-06-23 09:22:25
tags: sass
categories: 
- 前端
- sass
---
### sass
<!-- more -->
```
--watch style.scss:style.css
```

通过命令行及时更改scss对应的css

![sass](http://orzbvlxeq.bkt.clouddn.com/sass.png)

@mixin box-shadow($shadow...) {
  @if length($shadow) >= 1 {
    @include prefixer(box-shadow, $shadow);
  } @else{
    $shadow:0 0 4px rgba(0,0,0,.3);
    @include prefixer(box-shadow, $shadow);
  }
}

这个 box-shadow 的混合宏，带有多个参数，这个时候可以使用“ … ”来替代。简单的解释一下，当 $shadow 的参数数量值大于或等于“ 1 ”时，表示有多个阴影值，反之调用默认的参数值“ 0 0 4px rgba(0,0,0,.3) ”。

@mixin border-radius($radius){
  -webkit-border-radius: $radius;
  border-radius: $radius;
}

.box {
  @include border-radius(3px);
}
传一个不带值得参数
![sass](http://orzbvlxeq.bkt.clouddn.com/sassMixin.png)

函数列表
•       length($list)：返回一个列表的长度值；
•       nth($list, $n)：返回一个列表中指定的某个标签值
•       join($list1, $list2, [$separator])：将两个列给连接在一起，变成一个列表；
•       append($list1, $val, [$separator])：将某个值放在列表的最后；
•       zip($lists…)：将几个列表结合成一个多维的列表；
•       index($list, $value)：返回一个值在列表中的位置值。

Introspection函数
• type-of($value)：返回一个值的类型
• unit($number)：返回一个值的单位
• unitless($number)：判断一个值是否带有单位
• comparable($number-1, $number-2)：判断两个值是否可以做加、减和合并

map函数
• map-get($map,$key)：根据给定的 key 值，返回 map 中相关的值。
• map-merge($map1,$map2)：将两个 map 合并成一个新的 map。
• map-remove($map,$key)：从 map 中删除一个 key，返回一个新 map。
• map-keys($map)：返回 map 中所有的 key。
• map-values($map)：返回 map 中所有的 value。
• map-has-key($map,$key)：根据给定的 key 值判断 map 是否有对应的 value 值，如果有返回 true，否则返回 false。
• keywords($args)：返回一个函数的参数，这个参数可以动态的设置 key 和 value。


颜色函数

• rgb($red,$green,$blue)：根据红、绿、蓝三个值创建一个颜色；
• rgba($red,$green,$blue,$alpha)：根据红、绿、蓝和透明度值创建一个颜色；
• red($color)：从一个颜色中获取其中红色值；
• green($color)：从一个颜色中获取其中绿色值；
• blue($color)：从一个颜色中获取其中蓝色值；
• mix($color-1,$color-2,[$weight])：把两种颜色混合在一起。


• hsl($hue,$saturation,$lightness)：通过色相（hue）、饱和度(saturation)和亮度（lightness）的值创建一个颜色；
• hsla($hue,$saturation,$lightness,$alpha)：通过色相（hue）、饱和度(saturation)、亮度（lightness）和透明（alpha）的值创建一个颜色；
• hue($color)：从一个颜色中获取色相（hue）值；
• saturation($color)：从一个颜色中获取饱和度（saturation）值；
• lightness($color)：从一个颜色中获取亮度（lightness）值；
• adjust-hue($color,$degrees)：通过改变一个颜色的色相值，创建一个新的颜色；
• lighten($color,$amount)：通过改变颜色的亮度值，让颜色变亮，创建一个新的颜色；
• darken($color,$amount)：通过改变颜色的亮度值，让颜色变暗，创建一个新的颜色；
• saturate($color,$amount)：通过改变颜色的饱和度值，让颜色更饱和，从而创建一个新的颜色
• desaturate($color,$amount)：通过改变颜色的饱和度值，让颜色更少的饱和，从而创建出一个新的颜色；
• grayscale($color)：将一个颜色变成灰色，相当于desaturate($color,100%);
• complement($color)：返回一个补充色，相当于adjust-hue($color,180deg);
• invert($color)：反回一个反相色，红、绿、蓝色值倒过来，而透明度不变。
•  
• 
• 
• 
•   alpha($color) /opacity($color)：获取颜色透明度值；
•       rgba($color, $alpha)：改变颜色的透明度值；
•       opacify($color, $amount) / fade-in($color, $amount)：使颜色更不透明；
•       transparentize($color, $amount) / fade-out($color, $amount)：使颜色更加透明。


