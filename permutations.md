# Permutations



Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

&#x20;

**Example 1:**

```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**Example 2:**

```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

**Example 3:**

```
Input: nums = [1]
Output: [[1]]
```

&#x20;

**Constraints:**

* `1 <= nums.length <= 6`
* `-10 <= nums[i] <= 10`
* All the integers of `nums` are **unique**.

```
class Solution {
        vector<vector<int>> rs;
    public:

    void f(vector<int> nums,int index,vector<int> temp){
        if(index==nums.size()){
            this->rs.push_back(temp);
            return;
        }
        for(int i=index;i<nums.size();i++){
            temp[index] = nums[i];
            swap(nums[i],nums[index]);
            f(nums,index+1,temp);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
          vector<int> temp(nums.size());
        f(nums,0,temp);
            return this->rs;
    }
};
```
