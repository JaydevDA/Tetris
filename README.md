# A Simple Snake Game 🐍
- By Jaydev Dhabaliya 😎
- Dhruvir S Mayavat 😎
- Rashi Krishnani 👧🏻
- Rudrapratap Singh 😎

# Description 🔍

-Tetris is a classic puzzle that involves arranging falling geometric shapes, called tetrominoes, to create complete horizontal lines, which then disappear. The goal is to keep the playing field from filling up while aiming for a high score.   
-We will be using c++ as the coding language, and here is the step to step process to make the snake.

# Code Overview ⌨️🖥️

## Include Libraries 📚: 

#include <iostream> - OS Agnostic // for doing i/p and o/p operations  
#include <conio.h> - Non-OS Agnostic // for doing console i/p and o/p operations  
#include <windows.h> - Non-OS Agnostic // for system("cls")  
#include <ctime> - Non-OS Agnostic // for srand(time())

```
    #include <iostream>  
    #include <conio.h>  
    #include <windows.h>  
    #include <ctime>  
    using namespace std;  
```

## Declaring Variables 🔤 :
Values which will help in setting a graphical representation of the snake
- making a constant width of 40 units and length of 25 units.
- **bool gameover** - to end the game when one of the many conditions is met.
- **int Highscore** - to display the highscore of the overall game.
- **x,y and Xfruit,Yfruit** - Position of the head of the snake and a fruit respectively.
- **int score** - Declaring score as a variable.
- **int tailX[100] and tailY[100]** - to store the two dimensional position of elements in the tail.
- **int tLength** - declaring the length of the tail as a variable.
- **enum direction** - to declare enum of directions like left,up,down and right, and also stop.

```
const int width = 10;
const int height = 20;
bool gameOver;
int board[height][width] = {0};
int score = 0;  
int highScore = 0;  
int difficulty = 1;  
int speed = 300;  
```
