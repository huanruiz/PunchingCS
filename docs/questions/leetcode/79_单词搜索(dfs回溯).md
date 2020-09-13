dfs加回溯, 注意把dfs放在if中, 因为要探索各个方向. 并且方向可以用``[[0, 1], [0, -1], [1, 0], [-1, 0]]``这样的list来表示.
```
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        n = len(board)
        m = len(board[0])
        marked = [[False for j in range(m)] for i in range(n)]
        for i in range(n):
            for j in range(m):
                if self.dfs(board, marked, i, j, word, 0, m, n):
                    return True
        return False
    
    def dfs(self, board, marked, i, j, word, index, m, n):
        if index == len(word) - 1:
            return board[i][j] == word[index]
        
        if board[i][j] == word[index]:
            marked[i][j] = True
            for x, y in [[0, 1], [0, -1], [1, 0], [-1, 0]]:
                new_i = i + x
                new_j = j + y
                if new_i >= 0 and new_i < n and new_j >= 0 and new_j < m and not marked[new_i][new_j] and self.dfs(board, marked, new_i, new_j, word, index + 1, m, n):
                    return True
            marked[i][j] = False
        return False
```