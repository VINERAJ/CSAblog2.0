---
toc: true
comments: true
layout: post
title: Bad Translator
description: Learning javascript output
courses: { compsci: {week: 7} }
type: tangibles
---

<head>
    <title>Bad Translator</title>
</head>
<body>
    <textarea id="word-label" name="word-label" rows="1" cols="50"></textarea>
    <textarea id="translate-label" name="translate-label" rows="1" cols="50">Awaiting translation...</textarea>
    <button class="translate-button" id="translate-button" style="height:20px;width:100px">Translate!</button>
    <button class="new-word-button" id="new-word-button" style="height:20px;width:100px">New Word</button>
    <script>
        let wordList = ["quiero", "mucha", "baguette", "Krakenhausen", "sur", "debajo", "nagy", "veLLai", "aur", "singam", "deu", "feuer", "cicek", "itihas", "paaTTu", "prem"]
        let translateList = ["word", "bar", "about", "list", "Java", "east", "north", "west", "is", "completely", "gone", "history", "your", "to", "too", "town", "task", "lost", "bit", "bout", "depression", "flex", "saw"];
        function newWord() {
            randInt1 = Math.floor(Math.random()*16);
            wordGet = wordList[randInt1];
            document.getElementById("word-label").value = wordGet;
            document.getElementById("translate-label").value = "Awaiting translation...";
        }
        function translateWord() {
            randInt1 = Math.floor(Math.random()*24);
            translateGet = translateList[randInt1];
            document.getElementById("translate-label").value = translateGet;
        }
        newWord();
        document.getElementById("new-word-button").onclick = function(){
            newWord();
        };
        document.getElementById("translate-button").onclick = function(){
            translateWord();
        };
    </script>
</body>
