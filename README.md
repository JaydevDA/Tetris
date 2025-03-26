# A Simple tetris game 🧱
- By Jaydev Dhabaliya 😎
- Dhruvir S Mayavat 😎
- Rashi Krishnani 😎
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
Values which will help in setting a graphical representation of the grid
- we set a width of 10 units and a height of 20 units as given in the problem statement.
- **bool gameover** - to end the game when one of the many conditions is met.
- we set 0 for empty cells and 1 for non-empty cells.
- we intitially set score and highscore to 0.
- if no difficulty chosen by the user, we set the difficulty to easy(1.easy) by default.
- we set speed to 300 by default.

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

## Structuring the tetriminoes 🏗️
- We create a 3d array of tetriminoes A[a][b][c], where b and c are the x and y coordinates of the tetriminoes, and a is the no. of tetriminoes.
- For I shape, we construct a 4x4 cell structure, in which we set the top row to 1(filled) and the rest 0(empty).
- For O shape, we construct a 2x2 cell structure, in which we set all the cells to 1.
- For L shape, we construct a 2x3 cell structure, in which we set the top row and the 1st cell of the bottom row to 1 and the rest 0.
- for J shape, we construct a 2x3 cell structure, in which we set the top row and the last cell of the bottom row to 1 and the rest 0.
- for T shape, we construct a 2x3 cell structure, in which we set the middle cell of the top row and all cells in the bottom row to 1 and the rest 0.
- For S shape, we construct a 2x3 cell structure, in which we set the the first cell of the first row to 0 and the last cell of the second row to 0.
- For Z shape, we construct a 2x3 cell sturcture, in which we set the last cell of the first row to 0 and the first cell of the second row to 0.

```
int tetrominoes[7][4][4] = {
    {{1, 1, 1, 1}, {0, 0, 0, 0}, {0, 0, 0, 0}, {0, 0, 0, 0}},
    {{1, 1}, {1, 1}},
    {{0, 1, 0}, {1, 1, 1}},
    {{1, 1, 0}, {0, 1, 1}},
    {{0, 1, 1}, {1, 1, 0}},
    {{1, 1, 1}, {1, 0, 0}},
    {{1, 1, 1}, {0, 0, 1}}
};
```

## Running the program 🚀

- **srand(time(0))** is used to initialize the random number generator with a unique seed.
- we use while(true) to let the player choose if they want to restart.
- we ask the user to give an input for difficulty and take the input.
- if difficulty = 1 than speed to 400 and difficulty = 2 than speed to 250 else 100.
- we implement intitialGame() resets the game state to prepare for a new game session by clearing the game board, resetting scores, and generating the first block.
- gameLoop() is the core game loop of your Tetris-like game, handling user input, block movement, and game state updates until the game ends.
- we take an input y or n to restart the game. if y then we restart the game else we end it.
  

```
int main() {
    srand(time(0));
    while (true) {
        cout << "Select Difficulty: 1. Easy  2. Medium  3. Hard\n";
        cin >> difficulty;
        speed = (difficulty == 1) ? 400 : (difficulty == 2) ? 250 : 100;
        initializeGame();
        gameLoop();
        cout << "Play again? (y/n): ";
        char choice;
        cin >> choice;
        if (choice != 'y') break;
    }
    return 0;
}
```

