# Word Search

Given an `m x n` grid of characters `board` and a string `word`, return `true` _if_ `word` _exists in the grid_.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

&#x20;

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/11/04/word-1.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "SEE"
Output: true
```

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/15/word3.jpg)

```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCB"
Output: false
```

&#x20;

**Constraints:**

* `m == board.length`
* `n = board[i].length`
* `1 <= m, n <= 6`
* `1 <= word.length <= 15`
* `board` and `word` consists of only lowercase and uppercase English letters.

&#x20;

**Follow up:** Could you use search pruning to make your solution faster with a larger `board`?

**Explanation**

1. Start from each cell, and try to find the solution

When we call solve function, we use the following base conditions:

1. Boundary check for both i and j (that is currentRow && currentCol]
2. Is the given cell already visited
3. Is the given cell's character matches with the word\[k]
4. If the size of k >= (word.size()-1) as k is zero based index then return true

```
class Solution {
public:
    bool solve(vector<vector<char>>& board,int i,int j,string &word,int k){
        if(i<0 || j<0 || i>=board.size() || j>=board[0].size()) return false;
        if(board[i][j]=='$' || board[i][j]!=word[k]){
            return false;
        }
        if(k >= word.size()-1){
            return true;
        }
        
        char ch = board[i][j];
        board[i][j] = '$';
        bool left = solve(board,i,j-1,word,k+1);
        
        bool right =  solve(board,i,j+1,word,k+1);
            
        bool up =  solve(board,i-1,j,word,k+1);
            
        bool down = solve(board,i+1,j,word,k+1);
        board[i][j] = ch;
        return left || right || up || down;
    }
    bool exist(vector<vector<char>>& board, string word) {
        int m = board.size();
        int n = board[0].size();
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(solve(board,i,j,word,0)){
                    return true;
                }
            }
        }
        
        return false;
    }
};
```
