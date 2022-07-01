# 😁 Optimal Game strategy

There are two players P1 && P2.&#x20;

Rule:

The player can pick either the leftmost or the rightmost element of the array at the given point

First P1 gets to play

Goal: Achieve the max amount

What is the max amount that P1 can get

**Approach**

**for any given range the Player has two choices**

**Pick the leftmost or pick the rightmost**

**To make sure P1 gets the maximum sum then the we want that P2 will get the minimum total sum.**

**If P1 pick ith (leftmost) choice**

then the P2 can pick either i+1 or jth as it's next value we have to consider the minimum of these both case so that we can ensure P2 picks the minimum&#x20;

```
mini = min(optimalGameStrategy(arr,i+2,j),optimalGameStrategy(arr,i+1,j-1));
int choice1 = arr[i] + mini;
```

**If P1 picks jth (rightmost choice)**

then the P2 can pick either ith element or j-1 th element. Again ensure for both the paths P2 gets the minimum total in the range

```
int choice2 = arr[j] +
 min(optimalGameStrategy(arr,i+1,j-1),optimalGameStrategy(arr,i,j-2));
```

Code:

```
#include<iostream>
using namespace std;

int optimalGameStrategy(int arr[6], int i,int j){
    if(i >j) {
        return 0;
    }

    int choice1 = arr[i] + min(optimalGameStrategy(arr,i+2,j),optimalGameStrategy(arr,i+1,j-1));
    int choice2 = arr[j] + min(optimalGameStrategy(arr,i+1,j-1),optimalGameStrategy(arr,i,j-2));

    return max(choice1,choice2);
}

int main(){
    int arr[6] = {20,30,2,2,2,10};
    int size = 6;
    cout<<optimalGameStrategy(arr,0,size-1)<<endl;
    return 0;
}
```

