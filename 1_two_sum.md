# 1 two sum
### 1.暴力解法 
#### 即双重循环逐个匹配
##### 这种方法时间复杂度很高，但空间复杂度较低
##### C++实现
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        for(int i=0;i<nums.size();++i)
          for(int j=i+1;j<nums.size();++j){
              if(nums[i]+nums[j]==target)
              {
                  ans.push_back(i);
                  ans.push_back(j);
              }
          }
        return ans;
    }
};
```
##### python实现
```py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        length=len(nums)
        for i in range(length):
            for j in range(i+1,length):
                if nums[i]+nums[j]==target:
                    return [i,j]
```
