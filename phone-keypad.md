# Phone Keypad



Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in **any order**.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

&#x20;

**Example 1:**

```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**Example 2:**

```
Input: digits = ""
Output: []
```

**Example 3:**

```
Input: digits = "2"
Output: ["a","b","c"]
```

&#x20;

**Constraints:**

* `0 <= digits.length <= 4`
* `digits[i]` is a digit in the range `['2', '9']`.

```
#include<bits/stdc++.h>
using namespace std;
class Solution {
    map<char,string> s;
    vector<string> rs;
public:
    void initialize(){
        this->s.clear();
        this->rs.clear();
        s['0']="";
        s['1']="";
        s['2']="abc";
        s['3']="def";
        s['4'] ="ghi";
        s['5'] ="jkl";
        s['6'] ="mno";
        s['7'] ="pqrs";
        s['8'] = "tuv";
        s['9'] = "wxyz";
    }
    void f(string &digit,int index,  string op){
        if(index>=digit.size()){
            this->rs.push_back(op);
            return;
        }
        string temp;
        string letters = this->s[digit[index]];
        if(letters.size()==0) {
            f(digit,index+1,op);
        }
        for(int i=0;i<letters.size();i++){
             temp = op;
            temp.push_back(letters[i]);
            f(digit,index+1,temp);

        }
        
    }
    vector<string> letterCombinations(string digits) {
        
        initialize();
      //  cout<<this->s['2']<<endl;
       f(digits,0,"");
        return this->rs;
    }
};

int main(){
    Solution s;
    vector<string> rs = s.letterCombinations("234");
    for(int i=0;i<rs.size();i++){
        cout<<rs[i]<<endl;
    }
    return 0;
}
```
