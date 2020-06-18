<https://leetcode.com/problems/surrounded-regions/>

Firstly, replace all the `O`'s on the boarder or connected to `O`'s on the boarder with temporary markers `.` using a BFS approach with a queue. Then, replace all the remaining `O` with `X` and all the `.` with `O`.

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not any(board):
            return 
        rows, cols = len(board), len(board[0])
        
        queue = [pos for j in range(cols) for pos in ((0,j), (rows-1, j))]
        queue.extend([pos for i in range(rows) for pos in ((i,0), (i, cols-1))])
        while queue:
            i, j = queue.pop()
            if 0 <= i < rows and 0 <= j < cols and board[i][j] == 'O':
                board[i][j] = '.'
                queue.extend([(i+1, j), (i-1, j), (i, j+1), (i, j-1)])

        for i in range(rows):
            for j in range(cols):
                board[i][j] = ['X', 'O'][board[i][j] == '.']
        
```

