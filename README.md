# Surrounded Regions
## https://leetcode.com/problems/surrounded-regions

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.
```
Example:

X X X X
X O O X
X X O X
X O X X

After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
```
**Explanation:**

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.

## Approach :
We can solve this problem by first marking all the O's which are either on 4 borders or are connected to one of the O's, that is on the border. Because we don't have to flip these O's to X's. We can use a `visited` array to mark that we have already visited a cell.
We only have to flip O's which are completely surrounded by X's. 

To do that, now we will iterate over the board, starting from the second row and second column. And if we found both of the below 2 conditions to be true, then we will flip that O to X, also all of its unvisited neighbor cells which are O will be flipped to X.

1. Value at the cell is O
2. This cell is not already visited

![Surrounded Regions](surrounded-regions.PNG?raw=true "Surrounded Regions")

## Implementation 

```java
class Solution {
    public void solve(char[][] board) {
        if(board == null || board.length == 0)
            return;
     
        int rows = board.length;
        int cols = board[0].length;
        
        boolean[][] visited = new boolean[rows][cols];
        for(int j = 0; j < cols; j++) {
            if(board[0][j] == 'O')
                dfs(board, 0, j, visited, false);
            if(board[rows-1][j] == 'O')
                dfs(board, rows-1, j, visited, false);
        }
        for(int i = 0; i < rows; i++) {
            if(board[i][0] == 'O')
                dfs(board, i, 0, visited, false);
            if(board[i][cols-1] == 'O')
                dfs(board, i, cols-1, visited, false);
        }
        for(int i = 1; i < rows; i++) {
            for(int j = 1; j < cols; j++) {
                if(board[i][j] == 'O' && !visited[i][j])
                  dfs(board, i, j, visited, true); 
            }
        }
    }
    
    private void dfs(char[][] board, int row, int col, boolean[][] visited, boolean flip) {
        if(row < 0 || row >= board.length || col < 0 || col >= board[0].length)
            return;
        if(visited[row][col] || board[row][col] == 'X')
            return;
        if(flip)
            board[row][col] = 'X';
        
        visited[row][col] = true;
        dfs(board, row, col+1, visited, flip);
        dfs(board, row, col-1, visited, flip);
        dfs(board, row+1, col, visited, flip);
        dfs(board, row-1, col, visited, flip);
    }
}
```
