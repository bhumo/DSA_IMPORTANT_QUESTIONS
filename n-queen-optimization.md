# N Queen optimization

Here we will optimize the isSafe() before&#x20;

row check - > O(n)

left upper diagonal check -> O(n)

right diagonal check -> O(n)

**Row optimization**

**Map\<int,bool> Key: row index**

**Left Lower Diagonal Check optimization**

**Map\<int,bool> Key: row index + column index**

**Left upper** **Diagonal Check optimization**

**Map\<int,bool> Key: (n-1) + (column Index - row index)**

```
#include<bits/stdc++.h>
using namespace std;
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

bool isSafe(int n,int row,int column,map<int,bool> &rowMap, map<int,bool> &upperLeftDiagonal,map<int,bool> &lowerLeftDiagonal){
     // check for the left half of the row
     bool rowCheck = rowMap[row];    
    // check for upper diagonal in left part
    bool upperLeft = upperLeftDiagonal[(n-1)+(column-row)];
    // check for lower diagonal in left part
    bool lowerLeft =  lowerLeftDiagonal[row+column];
    // we are taking a false here because if the queen doesn't exists the map[key] will return false
    // false -> no queen
    // true -> queen is here
    return  !rowCheck && !upperLeft && !lowerLeft;
}
void  findAllTheWaysToPlaceNQueens(int column,int n,vector<vector<int>> &board,vector<vector<int>> &ans, map<int,bool> &rowMap,map<int,bool> &upperLeftDiagonal,map<int,bool> &lowerLeftDiagonal ){
    if(column==n){
        addToSolution(board,ans);
        return;
    }
    // traverse for all rows
    for(int i=0;i<n;i++){
        if(isSafe(n,i,column,rowMap,upperLeftDiagonal,lowerLeftDiagonal)){
            // place queen
            board[i][column]=1;
            rowMap[i]=true;
            lowerLeftDiagonal[i+column]=true;
            upperLeftDiagonal[(n-1)+(column-i)]=true;
            findAllTheWaysToPlaceNQueens(column+1,n,board,ans,rowMap,upperLeftDiagonal,lowerLeftDiagonal);
            //backtracking
            board[i][column]=0;
            rowMap[i]=false;
            lowerLeftDiagonal[i+column]= false;
            upperLeftDiagonal[(n-1)+(column-i)]= false;
            
        }
    }
}
vector<vector<int>> nQueens(int n)
{
	// Write your code here
    vector<vector<int>> board(n,vector<int>(n,0));
    vector<vector<int>> ans;
    map<int,bool> rowMaps;
    map<int,bool> upperLeftDiagonal;
    map<int,bool> lowerLeftDiagonal;
    findAllTheWaysToPlaceNQueens(0,n,board,ans,rowMaps,upperLeftDiagonal,lowerLeftDiagonal);
    return ans;
	
}
```
