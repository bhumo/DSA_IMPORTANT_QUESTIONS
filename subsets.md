# Subsets



Given an integer array `nums` of **unique** elements, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

&#x20;

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**

```
Input: nums = [0]
Output: [[],[0]]
```

&#x20;

**Constraints:**

* `1 <= nums.length <= 10`
* `-10 <= nums[i] <= 10`
* All the numbers of `nums` are **unique**

```
class Solution {
public:
    void generateSubset(vector<int>& nums, int i,int n,vector<vector<int>>&rs,vector<int> temp){
        if(i==n) {
            rs.push_back(temp);
            return;
        }
        // not adding the value in resultant
        generateSubset(nums,i+1,n,rs,temp);
        // adding the value in resultant
        temp.push_back(nums[i]);
        
        generateSubset(nums,i+1,n,rs,temp);
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> rs;
        f(nums,0,nums.size(),rs,vector<int>());
        return rs;
    }
};
```
