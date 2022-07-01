# Permutation in strings

Problem: Given the string in I/P find all the permutation of the string and print it in lexicographical order

I/P: "abc"

O/P : "abc" "acb" "bac" "bca" "cab" "cba"

```
#include<iostream>
#include<bits/stdc++.h>
using namespace std;

void permitutionInString(string s,int index, int n,vector<string> &rs){
    if(index==n){
        rs.push_back(s);
        return;
    }
    for(int i=index;i<n;i++){
        swap(s[i],s[index]);
        permitutionInString(s,index+1,n,rs);
        swap(s[i],s[index]);
    }
}
int main(){
    string s;
    cout<<"Enter String:";
    cin>>s;
    vector<string> rs;
    permitutionInString( s,0,s.size(),rs);
    // sort it for lexiographicall order
    sort(rs.begin(),rs.end());
    for(int i=0;i<rs.size();i++){
        cout<<rs[i]<<endl;
    }
    return 0;
}
```
