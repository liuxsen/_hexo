---
title: css3 @media_Rule
date: 2017-03-05 22:16:18
tags: css技巧
---


# @media 

```css
@media 
(-webkit-min-device-pixel-ratio: 2), 
(-webkit-min-device-pixel-ratio: 3){

} 
```

> 面向未来**高度兼容**的写法；


```css
@media
only screen and (-webkit-min-device-pixel-ratio: 2),
only screen and (   min--moz-device-pixel-ratio: 2),
only screen and (     -o-min-device-pixel-ratio: 2/1),
only screen and (        min-device-pixel-ratio: 2),
only screen and (                min-resolution: 192dpi),
only screen and (                min-resolution: 2dppx) { 
  
  /* Retina-specific stuff here */
  /*视网膜规则，或者说是高质量图片规则，放在这里*/

}
```

### sass mixin

> 通过判断清晰度（highish-res） 来动态添加高质量的图片；

```css
bg-image($url){
    background-image:url($url+"@2x.png");
    @media
        only screen and (-webkit-min-device-pixel-ratio: 3),
        only screen and (   min--moz-device-pixel-ratio: 3),
        only screen and (     -o-min-device-pixel-ratio: 3/1),
        only screen and (        min-device-pixel-ratio: 3),
        only screen and (                min-resolution: 300dpi),
        only screen and (                min-resolution: 3dppx) { 
          background-image: url($url+"@3x.png");
            /* Retina-specific stuff here */
            /*视网膜规则，或者说是高质量图片规则，放在这里*/
        }
}
```