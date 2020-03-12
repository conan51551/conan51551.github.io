---
title: 裁剪上传的图片
tags:
  - base
date: 2018-02-02 16:31:24
categories:
- 前端
- optimize
---

图片裁剪上传功能通用的方法(基于原生JS，不需要引入任何框架)
<!-- more -->
``` html
<!doctype html>
<html>

<head>
    <meta charset="UTF-8">
    <title>tailorPic</title>
</head>

<body>
    <input type="file" id="inputArea" style="display:none;" onchange="getImg()">
    <!-- 上传的原始图片 -->
    <canvas id="imgCanvas" alt=""></canvas>
    <!-- 裁剪过的图片 -->
    <canvas id="resultCanvas"></canvas>
</body>
<script>
    var imgFrom = document.getElementById("inputArea");

    function loadimg() {
        imgFrom.click();
    }

    function getImg() {
        var myFrom = new FormData();

        var imageData = imgFrom.files[0]; //获取表单中第一个文件

        myFrom.append("image", imageData); //向表单中添加一个键值对

        var reader = new FileReader(); //调用FileReader对象

        reader.readAsDataURL(imageData); //通过DataURL的方式返回图像

        var theCanvas = document.getElementById("imgCanvas");
        var canvasImg = theCanvas.getContext("2d");
        var img = new Image();

        reader.onload = function(e) {
            img.src = e.target.result;
        }
        img.onload = function() {
            theCanvas.width = img.width; //将img对象的长款赋给canvas标签

            theCanvas.height = img.height;

            canvasImg.drawImage(img, 0, 0);

            var resultCanvas = document.getElementById("resultCanvas");
            var resultImg = resultCanvas.getContext("2d");
            var flag = false;
            var W = theCanvas.width; //上传图片的宽度
            var H = theCanvas.height; //上传图片的高度
            var cutData; //裁剪过的DATA
            var startX = 0;
            var startY = 0;

            theCanvas.addEventListener("mousedown", function(e) {
                flag = true; //改变标记状态，置为点击状态
                startX = e.clientX; //获得起始点横坐标
                startY = e.clientY; //获得起始点纵坐标
                cutData = canvasImg.getImageData(0, 0, W, H);
                if (!!cutData) {
                    resultImg.clearRect(0, 0, cutData.width, cutData.height); //清空预览区域
                }
            })

            theCanvas.addEventListener("mousemove", function(e) {
                if (flag) {
                    canvasImg.clearRect(0, 0, W, H);
                    canvasImg.drawImage(img, 0, 0); //重新绘制图片
                    canvasImg.fillStyle = 'rgba(255,255,255,0.6)';
                    canvasImg.fillRect(0, 0, e.clientX, startY); //矩形A
                    canvasImg.fillRect(e.clientX, 0, W, e.clientY); //矩形B
                    canvasImg.fillRect(startX, e.clientY, W - startX, H - e.clientY); //矩形C
                    canvasImg.fillRect(0, startY, startX, H - startY); //矩形D
                }
            })
            theCanvas.addEventListener("mouseup", function(e) {
                cutData = canvasImg.getImageData(startX, startY, e.clientX - startX, e.clientY - startY); //截取黑框区域图片信息
                resultImg.putImageData(cutData, 0, 0); //将图片信息赋给预览区域
                resultCanvas.toBlob(function(blob) {
                    resultFile = blob; //上传的blob

                })
                flag = false;
            })
        }
    }
</script>

</html>

```