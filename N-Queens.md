---
name: N-Queens Problem
about: Solution and notes on N-Queens problem
title: ''
labels: C++, Hard
assignees: 'Shivam Patel'

---

# 

## Code
```cpp

#include <vector>
#include <string>

using namespace std;

class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> result;
        vector<int> board(n, -1);
        placeQueen(0, n, board, result);
        return result;
    }

private:
    bool isNotUnderAttack(int row, int col, const vector<int>& board) {
        for (int prevRow = 0; prevRow < row; ++prevRow) {
            if (board[prevRow] == col || 
                board[prevRow] - prevRow == col - row || 
                board[prevRow] + prevRow == col + row) {
                return false;
            }
        }
        return true;
    }

    void placeQueen(int row, int n, vector<int>& board, vector<vector<string>>& result) {
        if (row == n) {
            result.push_back(createBoard(board));
            return;
        }

        for (int col = 0; col < n; ++col) {
            if (isNotUnderAttack(row, col, board)) {
                board[row] = col;
                placeQueen(row + 1, n, board, result);
            }
        }
    }

    vector<string> createBoard(const vector<int>& board) {
        vector<string> result;
        for (int i = 0; i < board.size(); ++i) {
            string row(board.size(), '.');
            row[board[i]] = 'Q';
            result.push_back(row);
        }
        return result;
    }
};


```

## Notes

### N-Queens Problem Solution in C++

#### Problem Description
The N-Queens problem requires placing N queens on an N×N chessboard in such a way that no two queens threaten each other. The goal is to find all possible arrangements of queens satisfying this constraint.

#### Solution Overview
- **isNotUnderAttack(row, col, board):**
  - Checks whether placing a queen at the current position (row, col) is a valid move.
  - Examines the rows above the current row to ensure there is no threat.
  - Returns `true` if the placement is valid, `false` otherwise.

- **placeQueen(row, n, board, result):**
  - Uses backtracking to explore all possible configurations.
  - Places queens row by row, ensuring each placement is valid.
  - Calls the `isNotUnderAttack` function to validate queen placements.
  - Recursively explores the next row if the current placement is valid.

- **createBoard(board):**
  - Creates a vector of strings representing the chessboard.
  - "Q" represents a queen, and "." represents an empty cell on the chessboard.

- **Usage:**
  - Create an instance of the `Solution` class.
  - Call the `solveNQueens` method with the desired value of `n`.
  - The result is a vector of vector of strings representing the solutions.

    ```cpp
    Solution sol;
    int n = 4;
    std::vector<std::vector<std::string>> result = sol.solveNQueens(n);
    ```