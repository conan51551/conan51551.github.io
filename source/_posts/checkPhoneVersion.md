---
title: checkPhoneVersion
date: 2018-03-09 17:31:41
tags: tips
categories:
- 前端
- tips
---

有时需要判断设备的具体型号，可以通过cavas获取设备的显卡来判断
<!-- more -->
``` javascript
(function () {

    var canvas = document.createElement('canvas'),

        gl = canvas.getContext('experimental-webgl'),

        debugInfo = gl.getExtension('WEBGL_debug_renderer_info');

 

    console.log(gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL));

})();
```
