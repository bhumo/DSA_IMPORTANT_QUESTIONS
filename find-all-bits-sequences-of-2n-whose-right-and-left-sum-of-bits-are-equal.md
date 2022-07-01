# Find all bits sequences of 2n whose right & left sum of bits are equal

**Problem**

The problem states that given an number n, we have to find those sequences of 2n whose left & right sum of bits are equal.

I/P

n=2

O/P

&#x20;so the following are the sequences that can be made

Total no of combinations = 2n! = 2\*(2)! = 4! = 2\*2\*2\*2 = 16 combinations are possible

For a given binary 0110 -> 01 10 => left sum = 0+1=1 right sum=> 1 +0=1

| Sequences | Is left sum == right sum                                  | Count so far |
| --------- | --------------------------------------------------------- | ------------ |
| 0000      | 0 == 0                                                    | 1            |
|  0001     | 0 != 1 ( sum of 1 bits in left && sum of 1 bits in right) | 1            |
| 0010      | 0!=1                                                      | 1            |
| 0011      | 0!=2                                                      | 1            |
| 0100      | 1!=0                                                      | 1            |
|  0101     | 1==1                                                      | 2            |
| 0110      | 1==1                                                      | 3            |
| 0111      | 1!=2                                                      | 3            |
|  1000     | 1!=0                                                      | 3            |
|  1001     | 1==1                                                      | 4            |
| 1010      | 1==1                                                      | 5            |
| 1011      | 1!=2                                                      | 5            |
| 1100      | 2!=0                                                      | 5            |
| 1101      | 2!=1                                                      | 5            |
| 1110      | 2!=1                                                      | 5            |
| 1111      | 2==2                                                      | 6            |

So the output = 6

\[ 0101,1111,1001,0110,0000,1010]



1. Initialize ls & rs = 0
2. we have a array of 2n size, i points to leftmost part, j points to rightmost part
3. for two block i,j there are 4 ways -> (0,0),(0,1),(1,0),(1,1)&#x20;

TC: O(n!) which is huge.

```
#include<iostream>
using namespace std;
int equalLeftRightSumOfBits(int leftSum,int rightSum,char* arr,int i,int j){
    if(i>j){
        if(leftSum==rightSum) {
            cout<<arr<<endl;
            return 1;
        }
        return 0;
    }
    // call 0,0
    arr[i] = '0';
    arr[j] = '0';
    int call1 = equalLeftRightSumOfBits(leftSum+0,rightSum+0,arr,i+1,j-1);
    
    // call for 1,0
    arr[i] = '1';
    arr[j] = '0';
    int call2 = equalLeftRightSumOfBits(leftSum+1,rightSum+0,arr,i+1,j-1);

    //call for 0 1
    arr[i] = '0';
    arr[j] = '1';
    int call3 = equalLeftRightSumOfBits(leftSum+0,rightSum+1,arr,i+1,j-1);

    //call for 1,1
    arr[i] = '1';
    arr[j] = '1';
    int call4 = equalLeftRightSumOfBits(leftSum+1,rightSum+1,arr,i+1,j-1);

    return call1 + call2 + call3 + call4;
}
#include<iostream>
using namespace std;
int main(){
    int n;
    cin>>n;
    int twice_n = n *2;
    char *output = new char[twice_n];
    output[2*n]='\0';
    cout<<equalLeftRightSumOfBits(0,0,output,0,twice_n-1);
}
```
