# 😁 Coin change: the total number of ways that an amount of money

Problem

finding the total _number of ways_ that an _amount_ of money&#x20;

I/P

4 (amount)

\[1,2] (array)



O/P

3

\[1,1,1,1] , \[1,1,2], \[2,2]



Approach 1:

**Base Case 1: if amount == 0 then there's one way to make it that is by not adding any coins**

**Base Case 2: if amount<0 then there's zero way to make that amount**

**now for every coin we will call the recursive function**

```
#include<iostream>
using namespace std;

int noOfWays(int coins[2],int size,int amount){
    if(amount == 0 ){
        return 1;
    }

    if(amount < 0 ){
        return 0;
    }

    int ways  = 0 ;
    for(int i=0;i<size;i++){
        ways += noOfWays(coins,size,amount-coins[i]);
    }
    return ways;
} // this answer is wrong as it considers the way [1,2,1] , [2,1,1], [1,1,2]  
// as seperate ways which is wrong

int main(){
    int coins[2] = {1,2};
    int amount = 4;
    int size = 2;
    cout<<noOfWays(coins,size,amount);
    return 0;
}
```

****

**The above approach is wrong as for I/p 4, \[1,2] it will give output 5**

****

**Correct Approach**

**i will restrict the call suppose i is at index 1 (coin\[1] is 2) then now the recursive calls won't be made for (coin\[0] or anything as for loop will start with 1)**

```
#include<iostream>
using namespace std;

int noOfWays(int coins[2],int size,int amount,int index){
    if(amount == 0 ){
        return 1;
    }

    if(amount < 0 ){
        return 0;
    }

    int ways  = 0 ;
    for(int i=index;i<size;i++){
        ways += noOfWays(coins,size,amount-coins[i],i);
    }
    return ways;
}

int main(){
    int coins[2] = {1,2};
    int amount = 4;
    int size = 2;
    cout<<noOfWays(coins,size,amount,0);
    return 0;
}
```
