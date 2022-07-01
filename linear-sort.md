# Linear Sort

### Problem

Sort the given array using linear sort with the help of recursion

### Solution

1. call linear function recursively till it's index is less than n(size of the array)
2. for every element that is smaller or equal to current element in the right part (index+1,n) and swap it (arr\[index],arr\[swapIndex])
3. TC:O( $$n^2$$)

```
#include<iostream>
using namespace std;
void linearSort(int arr[7],int index,int n){
    if(index>=n) return;
    int swapIndex = index;
    for(int i=index+1;i<n;i++){
        if(arr[i]<=arr[index]){
            swapIndex = i;
        }
    }
    swap(arr[swapIndex],arr[index]);
    linearSort(arr,index+1,n);
}
int main(){
    int arr[11] = {1,3,2,4,5,6,7,8,7,8,1};
    int size = 11;
    linearSort(arr,0,size);
    for(int i=0;i<size;i++){
        cout<<arr[i]<<" ";
    }
    return 0;
}
```
