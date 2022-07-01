# Generalized Abbreviation

Problem Statement&#x20;

**You are given a string ‘STR’ consisting of English lowercase letters.**

**Your task is to find out all the generalised abbreviations of ‘STR’ and print an array/list of these abbreviations sorted in increasing order.**

**Note:**

```
A string is said to be a generalised abbreviations string of ‘STR’ if we remove a substring of length ‘X’ from ‘STR’ and put the number ‘X’ at the place of the removed substring.

We can not remove two consecutive substrings or we can say generalised abbreviations will never have two consecutive numbers.
```

**For example:**

```
If ‘STR’ = “abc”,
Sorted generalized abbreviations of ‘STR’ are: [“1b1”, “1bc”, “2c”, “3”, “a1c”, “a2”, “ab1”, “abc”].
```

**Input Format:**

```
The first line of input contains a single integer T, representing the number of test cases.
Then the T test cases follow.

The first and the only line of each test case contains a string ‘STR’.
```

**Output format:**

```
For every test case, print all the generalised abbreviations of ‘STR’ separated by a single space.

The output of each test case is printed in a separate line.
```

**Note :**

```
You don’t have to print anything. It has already been taken care of. Just implement the given function. 
```

**Constraints:**

```
1<= T <=10
1<= |STR| <= 20

Where |STR| is length of String 'STR'.

Time limit: 1 sec
```

**Sample Input 1:**

```
2
ab
xyz
```

**Sample Output 1:**

```
1b  2  a1  ab
1y1  1yz  2z  3  x1z   x2   xy1   xyz
```

**Explanation Of Sample Input 1:**

```
For test case 1:
"ab" can be written as {1b,  2,  a1,  ab}.

For test case 2:
"xyz" can be written as {1y1, 1yz,  2z,  3,  x1z,   x2,   xy1,   xyz}.
```

**Sample Input 2:**

```
2
n
code
```

**Sample Output 2:**

```
1 n
1o1e  1o2  1od1  1ode  2d1  2de  3e  4  c1d1  c1de  c2e  c3  co1e  co2  cod1  code 
```

**Explanation Of Sample Input 2:**

```
For test case 1:
"n" can be written as {1, n}.

For test case 2:
"code" can be written as {1o1e,  1o2,  1od1,  1ode, 2d1,  2de,  3e,  4,  c1d1,  c1de,  c2e,  c3,  co1e,  co2,  cod1,  code}.
```

```
#include<bits/stdc++.h>
void solve(string &s, string &op, vector<string> &rs, int index){
    if(index==s.size()){
        rs.push_back(op);
        return;
    }
    int size  = s.size();
    char ch = 's';
    int op_size = op.size();
    if(index>0) ch = op[op_size-1];
    int ch0 = (int)'0';
    int ch9 =(int)'9';
    string num;
    if((int)ch>=ch0 && (int)ch<=ch9){
        int x = 0;
        for(int i=op_size-1;i>=0;i--){
            ch = op[i];
            if((int)ch>=ch0 && (int)ch<=ch9){
               num.push_back(ch);
                x++;
               }
            else{
                break;
            }
        }
        string oldop = op;
        while(x){
            op.pop_back();
            x--;
        }
        std::reverse(num.begin(),num.end());
        int number = stoi(num)+1;
        num =to_string(number);
        
        op = op+num;
        solve(s,op,rs,index+1);
        op=oldop;
    }else{
        op.push_back('1');

        solve(s,op,rs,index+1);
        op.pop_back();
    }
    // including
    op.push_back(s[index]);
    solve(s,op,rs,index+1);
    op.pop_back();
}

vector < string > findAbbr(string & str) {
    // Write your code here.
    vector<string> rs;
    int index   = 0;
    string  op;
    solve(str,op,rs,index);
    sort(rs.begin(),rs.end());
    return rs;
}
```
