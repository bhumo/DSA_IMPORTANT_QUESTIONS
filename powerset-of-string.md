# PowerSet of string

I/P

s: "abc"

O/P

" "(empty string) , "a", "b", "c", "ab", "ac", "bc", "abc"

Produce the power set of string in any order

For any given character we have two choices

1\) add it to output

2\) do not add it output

```
#include<iostream>
using namespace std;

void powerSetString(string input,string output,int index){
    if(input[index]=='\0'){
        cout<<output<<endl;
        return ;
    }
    powerSetString(input,output,index+1);
    output.push_back(input[index]);
    powerSetString(input,output,index+1);
    return;
}
int main(){
    string s = "abc";
    powerSetString(s,"",0);
     return 0;
}
```
