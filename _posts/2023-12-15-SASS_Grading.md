---
toc: true
comments: true
layout: post
title: SASS grading
description: grading Akshat
courses: { compsci: {week: 15} }
type: hacks
---

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>SASS UI Demo</title>
  <link rel="stylesheet" href="styles.css"> <!-- Link to SASS file -->
  <style>
    body {
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
  </style>
</head>
<body>
  <div class="card">
    <h2>Card Title</h2>
    <p>This is a simple card component created with SASS.</p>
    <button class="btn">Click me</button>
  </div>

  <div class="card featured">
    <h2>Featured Card</h2>
    <p>This card has additional features.</p>
    <button class="btn">Click me</button>
  </div>
</body>
</html>