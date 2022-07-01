# Rat in Maze

Consider a rat placed at **(0, 0)** in a square matrix **** of order **N \* N**. It has to reach the destination at **(N - 1, N - 1)**. Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are **'U'(up)**, **'D'(down)**, **'L' (left)**, **'R' (right)**. Value 0 at a cell in the matrix represents that it is blocked and rat cannot move to it while value 1 at a cell in the matrix represents that rat can be travel through it.\
**Note**: In a path, no cell can be visited more than one time. If the source cell is 0, the rat cannot move to any other cell.

**Example 1:**

```
Input:
N = 4
m[][] = {{1, 0, 0, 0},
         {1, 1, 0, 1}, 
         {1, 1, 0, 0},
         {0, 1, 1, 1}}
Output:
DDRDRR DRDDRR
Explanation:
The rat can reach the destination at 
(3, 3) from (0, 0) by two paths - DRDDRR 
and DDRDRR, when printed in sorted order 
we get DDRDRR DRDDRR.
```

**Example 2:**

```
Input:
N = 2
m[][] = {{1, 0},
         {1, 0}}
Output:
-1
Explanation:
No path exists and destination cell is 
blocked.
```

**Your Task:**  \
You don't need to read input or print anything. Complete the function **printPath()** which takes **N** and 2D array **m\[ ]\[ ]** as input parameters and returns the list of paths in lexicographically increasing order. \
**Note:** In case of no path, return an empty list. The driver will output **"-1"** automatically.

**Expected Time Complexity:** O((3N^2)).\
**Expected Auxiliary Space:** O(L \* X), L = length of the path, X = number of paths.

**Constraints:**\
2 ≤ N ≤ 5\
0 ≤ m\[i]\[j] ≤ 1

```
class Solution{
    int columns = 0;
    int rows = 0;
    vector<string> rs;
    vector<string> directions = {"U","D","L","R"};
    public:
    void generatePaths(vector<vector<int>> m,int curRow,int curCol,string path){
        if(curRow<0 || curCol<0 || curRow>=this->rows || curCol>=this->columns) return;
        if(m[curRow][curCol]<=0) return;
        if(curRow==this->rows-1 && curCol == this->columns-1){
            this->rs.push_back(path);
            return;
        }
        int g = m[curRow][curCol];
        int row[] = {-1,1,0,0};
        int col[] = {0,0,-1,1};
        m[curRow][curCol]=-1;
        for(int i=0;i<4;i++){
            generatePaths(m,curRow+row[i],curCol+col[i],path+this->directions[i]);
        }
        //m[curRow][curCol]=g;
    }
    vector<string> findPath(vector<vector<int>> &m, int n) {
        // Your code goes here
        this->columns = n;
        this->rows = n;
        this->rs.clear();
        generatePaths(m,0,0,"");
        return this->rs;
    }
};

```
