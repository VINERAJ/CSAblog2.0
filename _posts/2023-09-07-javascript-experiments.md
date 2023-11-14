---
toc: true
comments: true
layout: post
title: JavaScript Experiments
description: Learning javascript output
courses: { compsci: {week: 4} }
type: tangibles
---
<head>
    <title>Javascript Experiments</title>
    <table></table>
</head>

<body>
    <button class="add-button" id="add-button" style="height:20px;width:100px">Add a value</button>
</body>

<script>
    let people = [
        { name: "Vinay", age: "17", grade: "12" },
        {name: "Colin", age: "16", grade: "11"}
    ];

    function generateTable(table, data) {
        let thead = table.createTHead();
        let row = thead.insertRow();
        for (let key of data) {
            let th = document.createElement("th");
            let text = document.createTextNode(key);
            th.appendChild(text);
            row.appendChild(th);
        }
        for (let element of people) {
        let dataRow = table.insertRow();
        for (key in element) {
        let cell = dataRow.insertCell();
        let text = document.createTextNode(element[key]);
        cell.appendChild(text);
        }
    }
    }

    // function createBox() {
    //     <body><input type="text" class="search" id="search" placeholder="Search"></body>
    // }

    let table = document.querySelector("table");
    let data = Object.keys(people[0]);
    generateTable(table, data);

    
</script>