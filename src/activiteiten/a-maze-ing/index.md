---
categories:
  - Activiteiten
tags:
  - CSS
  - HTML
  - JavaScript
  - Spel
---

# A-Maze-ing

```html
<html>
  <head>
    <meta charset="utf-8" />
    <title>All Hallow's Eve Maze</title>

    <style>
      body {
        align-items: center;
        background-color: black;
        display: flex;
        height: 100dvh;
        justify-content: center;
        margin: 0;
        width: 100dvw;
      }

      #maze {
        --maze-size: min(75dvh, 75dvw);
        --cell-size: calc(var(--maze-size) / var(--number-of-cells));

        position: relative;
        height: var(--maze-size);
        width: var(--maze-size);

        &.escaped h1 {
          display: block;
        }

        div {
          display: inline-flex;

          height: var(--cell-size);
          width: var(--cell-size);

          font-size: var(--cell-size);
          align-items: center;
          justify-content: center;
        }

        h1 {
          color: green;
          display: none;
          font-family: sans-serif;
          text-align: center;
        }

        #player {
          cursor: hand;

          position: absolute;
          top: calc(var(--player-cell-y, 0) * var(--cell-size));
          left: calc(var(--player-cell-x, 0) * var(--cell-size));
          transition: all 0.2s;

          span {
            display: none;
          }
        }
      }
    </style>
  </head>

  <body></body>

  <script></script>
</html>
```
