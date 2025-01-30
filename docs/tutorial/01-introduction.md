<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pixel War Game</title>
    <style>
        canvas {
            border: 2px solid black;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="800"></canvas>
    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        const pixelSize = 20; // Piksel boyutu
        const rows = canvas.height / pixelSize;
        const cols = canvas.width / pixelSize;
        const grid = Array.from({ length: rows }, () => Array(cols).fill(null)); // Harita ızgarası

        // Oyuncu rengi
        const playerColor = 'blue';
        let playerX = Math.floor(cols / 2);
        let playerY = Math.floor(rows / 2);

        // Haritayı çizme fonksiyonu
        function drawGrid() {
            for (let row = 0; row < rows; row++) {
                for (let col = 0; col < cols; col++) {
                    if (grid[row][col]) {
                        ctx.fillStyle = grid[row][col];
                        ctx.fillRect(col * pixelSize, row * pixelSize, pixelSize, pixelSize);
                    }
                }
            }
        }

        // Oyuncu hareketi
        function movePlayer(x, y) {
            if (x >= 0 && x < cols && y >= 0 && y < rows) {
                grid[playerY][playerX] = null; // Eski pozisyonu temizle
                playerX = x;
                playerY = y;
                grid[playerY][playerX] = playerColor; // Yeni pozisyona oyuncuyu yerleştir
                drawGrid();
            }
        }

        // Klavye ile hareket
        document.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowUp') movePlayer(playerX, playerY - 1);
            if (e.key === 'ArrowDown') movePlayer(playerX, playerY + 1);
            if (e.key === 'ArrowLeft') movePlayer(playerX - 1, playerY);
            if (e.key === 'ArrowRight') movePlayer(playerX + 1, playerY);
        });

        // Başlangıçta haritayı çiz
        grid[playerY][playerX] = playerColor;
        drawGrid();
    </script>
</body>
</html>
---
title: Tutorial - Introduction
sidebar_label: Introduction
slug: introduction
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Getting started

Welcome to the Socket.IO tutorial!

In this tutorial we'll create a basic chat application. It requires almost no basic prior knowledge of Node.JS or Socket.IO, so it’s ideal for users of all knowledge levels.

## Introduction

Writing a chat application with popular web applications stacks like LAMP (PHP) has normally been very hard. It involves polling the server for changes, keeping track of timestamps, and it’s a lot slower than it should be.

Sockets have traditionally been the solution around which most real-time chat systems are architected, providing a bi-directional communication channel between a client and a server.

This means that the server can *push* messages to clients. Whenever you write a chat message, the idea is that the server will get it and push it to all other connected clients.

## How to use this tutorial

### Tooling

Any text editor (from a basic text editor to a complete IDE such as [VS Code](https://code.visualstudio.com/)) should be sufficient to complete this tutorial.

Additionally, at the end of each step you will find a link to some online platforms ([CodeSandbox](https://codesandbox.io) and [StackBlitz](https://stackblitz.com), namely), allowing you to run the code directly from your browser:

![Screenshot of the CodeSandbox platform](/images/codesandbox.png)

### Syntax settings

In the Node.js world, there are two ways to import modules:

- the standard way: ECMAScript modules (or ESM)

```js
import { Server } from "socket.io";
```

Reference: https://nodejs.org/api/esm.html

- the legacy way: CommonJS

```js
const { Server } = require("socket.io");
```

Reference: https://nodejs.org/api/modules.html

Socket.IO supports both syntax. 

:::tip

We recommend using the ESM syntax in your project, though this might not always be feasible due to some packages not supporting this syntax.

:::

For your convenience, throughout the tutorial, each code block allows you to select your preferred syntax:

<Tabs groupId="lang">
  <TabItem value="cjs" label="CommonJS" default>

```js
const { Server } = require("socket.io");
```

  </TabItem>
  <TabItem value="mjs" label="ES modules">

```js
import { Server } from "socket.io";
```

  </TabItem>
</Tabs>


Ready? Click "Next" to get started.
