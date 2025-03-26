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

## Constructing the tetriminoes 🏗️
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

- We create a struct Block, which comprises of shape, size and the position of a block.
- **int shape[4][4]** - The 4x4 matrix representing the block's shape
- **int size** - The size of the block (3x3 or 4x4)
- **int x,y** - The block's position on the board

```
struct Block {
    int shape[4][4];  
    int size;         
    int x, y;
} currentBlock; 
```

## Functions used 📊

### void copyShape()
- This function copyShape()  is used to copy a Tetromino shape into a 4x4 matrix in a Tetris-like game. Here's a brief breakdown:

- Function Definition
   void copyShape(int shape[4][4], int id)` declares the function with a 4x4 matrix shape as the target and an integer id to select the Tetromino.

- Shape Copying:
   shape[i][j] = tetrominoes[id][i][j]  assigns the value from the tetrominoes array (selected by id) to the corresponding cell in shape.

- Ensures that the game correctly assigns a new block when generating one.

This function is used in generateBlock() to set up a new tetromino when needed.

```
void copyShape(int shape[4][4], int id) {
    for (int i = 0; i < 4; i++){
        for (int j = 0; j < 4; j++){
            shape[i][j] = tetrominoes[id][i][j];
        }
    }    
}
```

### void generateBlock()
- This function generateBlock() is used to create a new block in a Tetris-like game. Here's a brief breakdown:

- Random Block Selection:

rand() % 7 picks a random number between 0 and 6, representing one of the 7 classic Tetris block shapes (e.g., I, J, L, O, S, T, Z).

- Shape Assignment:

copyShape(currentBlock.shape, id) copies the selected block shape into currentBlock.

- Size Determination:

The I-block (id == 0) is 4 units long so size is equal to 4, the rest can fit in size = 3, thus 3 otherwise.

- Positioning:

The block is centered at the top of the game grid (x = width / 2 - 1, y = 0).
```
void generateBlock() {
    int id = rand() % 7;
    copyShape(currentBlock.shape, id);
    currentBlock.size = (id == 0) ? 4 : 3;
    currentBlock.x = width / 2 - 1;
    currentBlock.y = 0;
}
```

### void initializeGame()
- gameover is initially set to false and the score to zero.
- Here we set the contents of the grid.
- Initially the grid is empty, thus setting all the cells to zero.
- The generateBlock() function call generates the first tetromino (block) at the start of the game.

Since the game board is empty at the beginning, we need to spawn an initial block for the player to control.

Without this line, the game would start with an empty board and no falling piece.
  
```
void initializeGame() {
    gameOver = false;
    score = 0;
    for (int i = 0; i < height; i++)
        for (int j = 0; j < width; j++)
            board[i][j] = 0;
    generateBlock();
}
```

### void drawBoard()
- This function drawBoard() is responsible for rendering the Tetris game board in the console. Here's a brief breakdown:

- Reset Cursor Position:

Moves the console cursor to (0, 0) to overwrite the previous frame (for smooth animation).

- Create a Temporary Board:

Copies the main board into tempBoard to avoid modifying the original grid.

- Draw the Current Block:

Overlays the currentBlock onto tempBoard at its current position (x, y).

Only draws the block's filled cells (1) if they are within visible bounds (currentBlock.y + i >= 0).

- Render the Board:

Prints each cell of tempBoard:

for filled cells (blocks)

(space) for empty cells

Borders (|) are added on both sides for visual clarity.

- Display Game Info:  

Shows the current score, high score, and difficulty level (Easy/Medium/Hard).

```
void drawBoard() {
    COORD cursorPosition = {0, 0};
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), cursorPosition);
    int tempBoard[height][width];
    for (int i = 0; i < height; i++)
        for (int j = 0; j < width; j++)
            tempBoard[i][j] = board[i][j];
    for (int i = 0; i < currentBlock.size; i++) {
        for (int j = 0; j < currentBlock.size; j++) {
            if (currentBlock.shape[i][j] && currentBlock.y + i >= 0) {
                tempBoard[currentBlock.y + i][currentBlock.x + j] = 1;
            }
        }
    }
    for (int i = 0; i < height; i++) {
        cout << "| ";
        for (int j = 0; j < width; j++) {
            cout << (tempBoard[i][j] ? "#" : " ") << " ";
        }
        cout << "|" << endl;
    }
    cout << "Score: " << score << " | High Score: " << highScore << " | Difficulty: " << (difficulty == 1 ? "Easy" : difficulty == 2 ? "Medium" : "Hard") << endl;
}
```

### bool IsValidMove(int NewX, int NewY)
- newX and NewY is the new position to check for validity
- this function iterates through the block's shape (a 2D array where 1 represents part of the block).

- Check each cell of the block – if it's part of the block (currentBlock.shape[i][j] is true), calculate its new position (nx, ny).

- Check for collisions:

- If the new position is outside the left/right boundaries (nx < 0 or nx >= width).

- If the new position is below the bottom (ny >= height).

- If the new position overlaps with an occupied cell on the board (ny >= 0 && board[ny][nx] is true).

- Return false if any collision is detected, otherwise return true (move is valid).

```
bool isValidMove(int newX, int newY) {
    for (int i = 0; i < currentBlock.size; i++) {
        for (int j = 0; j < currentBlock.size; j++) {
            if (currentBlock.shape[i][j]) {
                int nx = newX + j, ny = newY + i;
                if (nx < 0 || nx >= width || ny >= height || (ny >= 0 && board[ny][nx]))
                    return false;
            }
        }
    }
    return true;
}
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

