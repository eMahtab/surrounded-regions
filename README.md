# Surrounded Regions



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
