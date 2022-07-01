# Find maximum in the array

```
// Some code
#include<iostream>
#include<limits.h>
using namespace std;

int findMax(int arr[5],int index,int n){
    if(index >= n) return INT_MIN;
    return max(arr[index],findMax(arr,index+1,n));
}
int main(){
    int arr[6] = {8,4,5,6,7,12};
    cout<<findMax(arr,0,6)<<endl;
}
```
