---
toc: true
comments: true
layout: post
title: Fibonacci JavaScript Version
description: Fibo project but in javascript
courses: { compsci: {week: 15} }
type: tangibles
---

<head>
</head>
<body>
    <input type="text" id="list-len" placeholder="Input a number">
    <button class="Go" id="fibo-button">Go!</button>
    <button class="Delete" id="delete-button">Reset Table</button>
    <table>
        <thead>
        <tr>
            <th colspan=4>The Fibonacci Sequence</th>
        </tr>
        </thead>
        <tbody>
            <tr>
                <td>Method</td>
                <td>Complexity</td>
                <td>Length of List</td>
                <td>List</td>
            </tr>
            <!-- <tr>
                <td>For</td>
                <td>Complexity</td>
                <td>Length of List</td>
                <td>List</td>
            </tr> -->
        </tbody>
        <tbody id=body2>
        </tbody>
    </table>
    <script>
        var fiboList = [];
        fiboList.push(0);
        fiboList.push(1);
        function forFibo(n) {
            if (n <= 0) {
                return 'Invalid input. N should be a positive integer.';
            }
            const startTime = performance.now();
            for (let i = 2; i <= n; i++) {
            fiboList[i] = fiboList[i - 1] + fiboList[i - 2];
            }
            const endTime = performance.now();
            const elapsedTime = endTime - startTime;
            return {
                sequence: fiboList.slice(0, n + 1),
                time: elapsedTime.toFixed(5) + ' milliseconds',
            };
        }
        function fibonacciWhile(n) {
    if (n <= 0) {
        return 'Invalid input. N should be a positive integer.';
    }
    let fibSequence = [0, 1];
    let i = 2;
    const startTime = performance.now();
    while (i <= n) {
        fibSequence[i] = fibSequence[i - 1] + fibSequence[i - 2];
        i++;
    }
    const endTime = performance.now();
    const elapsedTime = endTime - startTime;
    return {
        sequence: fibSequence.slice(0, n + 1),
        time: elapsedTime.toFixed(5) + ' milliseconds',
    };
}
        function fibonacciRecursive(n) {
    if (n <= 0) {
        return 'Invalid input. N should be a positive integer.';
    }
    const fibSequence = [];
    const startTime = performance.now();
    function calculateFibonacci(i) {
        if (i <= n) {
            if (i === 0) {
                fibSequence[i] = 0;
            } else if (i === 1) {
                fibSequence[i] = 1;
            } else {
                fibSequence[i] = fibSequence[i - 1] + fibSequence[i - 2];
            }
            calculateFibonacci(i + 1);
        }
    }
    calculateFibonacci(0);
    const endTime = performance.now();
    const elapsedTime = endTime - startTime;
    return {
        sequence: fibSequence.slice(0, n + 1),
        time: elapsedTime.toFixed(5) + ' milliseconds',
    };
}
function* fibonacciStream() {
    let a = 0, b = 1;
    while (true) {
        yield a;
        [a, b] = [b, a + b];
    }
}
function calculateFibonacciStream(n) {
    if (n <= 0) {
        return 'Invalid input. N should be a positive integer.';
    }
    const fibSequence = [];
    const fibGenerator = fibonacciStream();
    const startTime = performance.now();
    for (let i = 0; i <= n; i++) {
        fibSequence.push(fibGenerator.next().value);
    }
    const endTime = performance.now();
    const elapsedTime = endTime - startTime;
    return {
        sequence: fibSequence,
        time: elapsedTime.toFixed(5) + ' milliseconds',
    };
}
        function go() {
            //for loop
            var fiboLen = document.getElementById("list-len").value;
            const resultFor = forFibo(fiboLen-1);
            // for (let i = 0; i < 4; i++) {
                const row = document.createElement("tr");
                const cell1 = document.createElement("td");
                // var methodNum = i + 1;
                const cellText1 = document.createTextNode("For");
                cell1.appendChild(cellText1);
                row.appendChild(cell1);
                const cell2 = document.createElement("td");
                const cellText2 = document.createTextNode(resultFor.time);
                cell2.appendChild(cellText2);
                row.appendChild(cell2);
                const cell3 = document.createElement("td");
                const cellText3 = document.createTextNode(fiboLen);
                cell3.appendChild(cellText3);
                row.appendChild(cell3);
                fiboList = resultFor.sequence;
                const cell4 = document.createElement("td");
                const cellText4 = document.createTextNode("[" + fiboList + "]");
                cell4.appendChild(cellText4);
                row.appendChild(cell4);
                body2.appendChild(row);
                //while loop
                const resultWhile = fibonacciWhile(fiboLen-1);
                const row2 = document.createElement("tr");
                const cellW = document.createElement("td");
                // var methodNum = i + 1;
                const cellTextW = document.createTextNode("While");
                cellW.appendChild(cellTextW);
                row2.appendChild(cellW);
                const cellX = document.createElement("td");
                const cellTextX = document.createTextNode(resultWhile.time);
                cellX.appendChild(cellTextX);
                row2.appendChild(cellX);
                const cellY = document.createElement("td");
                const cellTextY = document.createTextNode(fiboLen);
                cellY.appendChild(cellTextY);
                row2.appendChild(cellY);
                fiboList = resultWhile.sequence;
                const cellZ = document.createElement("td");
                const cellTextZ = document.createTextNode("[" + fiboList + "]");
                cellZ.appendChild(cellTextZ);
                row2.appendChild(cellZ);
                body2.appendChild(row2);
                //recursion
                const resultRecursive = fibonacciRecursive(fiboLen-1);
                const row3 = document.createElement("tr");
                const cellW1 = document.createElement("td");
                // var methodNum = i + 1;
                const cellTextW1 = document.createTextNode("Recursive");
                cellW1.appendChild(cellTextW1);
                row3.appendChild(cellW1);
                const cellX1 = document.createElement("td");
                const cellTextX1 = document.createTextNode(resultRecursive.time);
                cellX1.appendChild(cellTextX1);
                row3.appendChild(cellX1);
                const cellY1 = document.createElement("td");
                const cellTextY1 = document.createTextNode(fiboLen);
                cellY1.appendChild(cellTextY1);
                row3.appendChild(cellY1);
                fiboList = resultRecursive.sequence;
                const cellZ1 = document.createElement("td");
                const cellTextZ1 = document.createTextNode("[" + fiboList + "]");
                cellZ1.appendChild(cellTextZ1);
                row3.appendChild(cellZ1);
                body2.appendChild(row3);
                // Stream
                const resultStream =  calculateFibonacciStream(fiboLen-1);
                const row4 = document.createElement("tr");
                const cellW11 = document.createElement("td");
                // var methodNum = i + 1;
                const cellTextW11 = document.createTextNode("Stream");
                cellW11.appendChild(cellTextW11);
                row4.appendChild(cellW11);
                const cellX11 = document.createElement("td");
                const cellTextX11 = document.createTextNode(resultStream.time);
                cellX11.appendChild(cellTextX11);
                row4.appendChild(cellX11);
                const cellY11 = document.createElement("td");
                const cellTextY11 = document.createTextNode(fiboLen);
                cellY11.appendChild(cellTextY11);
                row4.appendChild(cellY11);
                fiboList = resultStream.sequence;
                const cellZ11 = document.createElement("td");
                const cellTextZ11 = document.createTextNode("[" + fiboList + "]");
                cellZ11.appendChild(cellTextZ11);
                row4.appendChild(cellZ11);
                body2.appendChild(row4);
            }
        // }
        function resetTable() {
            const element = document.getElementById("body2");
            while (element.firstChild) {
            element.removeChild(element.firstChild);
            }
        }
        document.getElementById("fibo-button").onclick = function(){
            go();
        }
        document.getElementById("delete-button").onclick = function(){
            resetTable();
        }
    </script>
</body>