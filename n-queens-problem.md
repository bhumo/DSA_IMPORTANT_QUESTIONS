# N Queens Problem

**The N Queens puzzle is the problem of placing N chess queens on an N \* N chessboard such that no two queens attack each other.**

**Given an integer ‘N’, print all distinct solutions to the ‘N’ queen puzzle.**

```
Two queens on the same chessboard can attack each other if any of the below condition satisfies:  
1. They share a row. 
2. They share a column. 
3. They share a diagonal. 
```

**Input Format:**

```
The first line contains an integer 'T' which denotes the number of test cases. Then the test cases follow.

The first and the only line of each test case contains an integer ‘N’ denoting the size of the chessboard. 
```

**Output Format**

```
For each test case, print all the possible solutions, each in a new line. 

Each line would be representing a single configuration.

Each configuration would contain N * N elements printed row-wise separated by spaces. The position where we can place the queen will have the value 1, rest will have the value 0.

The sequence of the configurations returned does not matter. 

The output of each test case is printed in a separate line. 
```

**Note :**

```
You do not need to print anything, it has already been taken care of. Just implement the given function.  
```

**Constraints :**

```
1 <= T <= 10
1 <= N <= 10

Time Limit : 1 sec
```

**Sample Input 1:**

```
1
4   
```

**Sample Output 1:**

```
0 0 1 0 1 0 0 0 0 0 0 1 0 1 0 0
0 1 0 0 0 0 0 1 1 0 0 0 0 0 1 0 
```

**Explanation for Sample Input 1:**

```
The 4 queens can be placed in two ways in a 4*4 chessboard. Both the configurations are shown in the below figure. 
```

![](https://files.codingninjas.in/queens-6663.png)

```
The chessboard matrix for the first configuration looks as follows:-
0 0 1 0
1 0 0 0
0 0 0 1
0 1 0 0
Queen contained cell is depicted by 1. As we can see, No queen is in the same row, column or diagonal of the other queens. Hence this is a valid configuration.

Similarly, the chessboard matrix for the second configuration looks as follows:-
0 1 0 0
0 0 0 1
1 0 0 0
0 0 1 0
Queen contained cell is depicted by 1. As we can see, No queen is in the same row, column or diagonal of the other queens. Hence this is also a valid configuration.

These are the only two valid configurations for 4-Queens. 
```

**Sample Input 2:**

```
1
3
```

**Sample Output 2:**

```
```

**Explanation of Sample Input 2:**

```
Since no possible configuration exists for 3 Queen's, the output remains empty. 
```

![Prev](https://s3-ap-southeast-1.amazonaws.com/codestudio.codingninjas.com/codestudio/assets/icons/left-arrow.svg)\


```
#include<bits/stdc++.h>
using namespace std;

// Problem link: https://www.codingninjas.com/codestudio/problems/the-n-queens-puzzle_981286?topList=love-babbar-dsa-sheet-problems&leftPanelTab=1&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar
void addToSolution(vector<vector<int>> &board,vector<vector<int>> &ans)
{
    vector<int> temp;
 int n = board.size();   
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            temp.push_back(board[i][j]);
        }
    }
    ans.push_back(temp);
    return;
}

bool isSafe(int row,int column,vector<vector<int>> &board){
    int x = row;
    int y = column;
    int n = board.size();
    // check for the left half of the row
    while(y>=0){
        if(board[row][y]==1){
            return false;
        }
        y--;
    }
    
    // check for upper diagonal in left part
    
    x = row;
    y = column;
    while(x>=0 && y>=0){
        if(board[x][y]==1){
            return false;
        }
        x--;
        y--;
    }
    
    // check for lower diagonal in left part
    x = row;
    y = column;
    while(x<n && y<n){
        if(board[x][y]==1){ 
            return false;
        }
        x++;
        y--;
    }
    return true;
}
void  findAllTheWaysToPlaceNQueens(int column,int n,    vector<vector<int>> &board,vector<vector<int>> &ans ){
    if(column==n){
        addToSolution(board,ans);
        return;
    }
    // traverse for all rows
    for(int i=0;i<n;i++){
        if(isSafe(i,column,board)){
            // place queen
            board[i][column]=1;
            findAllTheWaysToPlaceNQueens(column+1,n,board,ans);
            //backtracking
            board[i][column]=0;
            
        }
    }
}
vector<vector<int>> nQueens(int n)
{
	// Write your code here
    vector<vector<int>> board(n,vector<int>(n,0));
    vector<vector<int>> ans;
    
    findAllTheWaysToPlaceNQueens(0,n,board,ans);
    return ans;
	
}
```
