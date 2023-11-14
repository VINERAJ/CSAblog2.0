---
toc: true
comments: true
layout: post
title: Moving Image
description: Learning javascript output
courses: { compsci: {week: 9} }
type: tangibles
---

<head>
    <title>Moving Image</title>
</head>
<body>
    <button class="move-button" id="move-button" style="height:20px;width:150px">Move the image!</button>
    <button class="return-button" id="return-button" style="height:20px;width:150px">Start over</button>
    <img src="/CSAblog/images/logo.png" id = "image" alt="drawing" width="200"/>
    <script>
        function move() {
            var x = document.getElementById("image").offsetLeft;
            var y = document.getElementById("image").offsetTop;
            randX = Math.floor(Math.random());
            randY = Math.floor(Math.random());
            document.getElementById("image").style.marginLeft = (x+randX) + 'px';
            document.getElementById("image").style.marginTop = (y+randY) + 'px';
            // await new Promise(r => setTimeout(r, 2));
        }
        function backToStart() {
            document.getElementById("image").style.marginLeft = '10px';
            document.getElementById("image").style.marginTop = '10px';
        }
        document.getElementById("move-button").onclick = function(){
            move();
        };
        document.getElementById("return-button").onclick = function(){
            backToStart();
        };
    </script>
</body>