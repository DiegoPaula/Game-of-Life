![Badge](https://img.shields.io/github/license/DiegoPaula/Game-of-Life)
![Badge](https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Ftwitter.com%2FDiegoPa49269521)

# Game-of-Life
This is my take on Conway's "Game of Life" using Vue.js

# Description
I built this project to further explore my knowledge of vue.js
Despite its simple and straightforward rules, Conway's game of life requires some creative solutions to work.

Game of life rules:
  -  Any live cell with fewer than two live neighbours dies, as if by underpopulation.
  -  Any live cell with two or three live neighbours lives on to the next generation.
  -  Any live cell with more than three live neighbours dies, as if by overpopulation.
  -  Any dead cell with exactly three live neighbours becomes a live cell, as if by reproduction.

![Gif](https://raw.githubusercontent.com/DiegoPaula/Game-of-Life/main/GoL.gif)

# Installation
To start it is necessary to clone the GitHub project in a directory of your choice:

```shell
cd "your_directory"
git clone https://github.com/DiegoPaula/Game-of-Life
```
After cloning the project, you need to install all dependencies:

```shell
cd "your_directory"\Game-of-Life-main\game-of-life
npm install
```

# Usage
After installing the project you can now run it on the development server:

```shell
cd "your_directory"\Game-of-Life-main\game-of-life\src
npm run serve
```
