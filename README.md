# LeetCode
LeetCode题解（正在更新中...）
### 217存在重复元素
#### 1. 暴力破解
```class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        for(int i;i<nums.size();i++){
            if(nums[i]==nums[i+1]){
                return true;
            }
        }
        return false;
    }
};
```
#### 2. 哈希表
```class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_set<int> set;
        for(auto num: nums){
            if(set.find(num)!=set.end()){
                return true;
            }
            set.insert(num); 
        }
        return false;
    }
};
```
### 136 只出现一次的数字
#### 按位异或
```class Solution {
public:
    int singleNumber(vector<int>& nums) {
        for(int i=1;i<nums.size();i++){
            nums[0]=nums[0]^nums[i];
        }
        return nums[0];
    }
};
```
### 169 多数元素
#### 排序后，出现次数大于n/2的元素，一定在中间位置上
```
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int length=nums.size();
        return nums[length/2];
    }
};
```
