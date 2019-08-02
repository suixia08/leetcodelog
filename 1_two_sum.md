# 1 two sum
---
### 1.暴力解法 
> 即双重循环逐个匹配

##### C++
> 时间复杂度o(n²)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
//注意不能直接声明数组，直接声明的数组是在栈中
//需要动态分配堆上的内存
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
##### python
```py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        length=len(nums)
        for i in range(length):
            for j in range(i+1,length):
                if nums[i]+nums[j]==target:
                    return [i,j]
```
---
### 2.双指针解法
>首先对数组进行排序，然后需要两个指针，一个low指向数组起始，一个high指向数组末端,然后判断nums[low]+nums[high]是否等于target.如果其值大于target,说明high所值的值太大，因此将high-1左移，再次判断，如果再次相加的值小于target值，则将low+1右移，然后再次判断相加的值，重复上述过程直至等于target值，将其low和high返回。



##### C++
>时间复杂度o(n)
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;//存储答案
        vector<int> nums_copy=nums;//复制数组
        //因为排序后原数值对应的下标会变
        int low=0;//指向起点
        int high=nums.size()-1;//指向末端
        int sum; //计算和用于比较
        sort(nums.begin(),nums.end());//排序
        sum=nums[low]+nums[high];
        while(sum!=target){
            if(sum>target) high-=1;
            if(sum<target) low+=1;
            sum=nums[low]+nums[high];
    }
    //下面的两个for是用来确定得到的值在原数组中的位置
       for(int i=0;i<nums.size();i++)
           if(nums_copy[i]==nums[low]){
               ans.push_back(i);
               break;
           }
        
         for(int j=nums.size()-1;j>=0;j--)
           if(nums_copy[j]==nums[high]){
               ans.push_back(j);
               break;
           }
    
           
        return ans;
    }
};
```
##### python
>这个代码是正确的，但是submit后超时了，思路和上面的一模一样，事实证明python不适合这样写。
```py
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums_copy=nums
        nums.sort()
        numSize=len(nums)
        low=0
        high=numSize-1
        sum=nums[low]+nums[high]
        while sum!=target:
            if sum>target:
                --high
            elif sum<target:
                ++low
            sum=nums[low]+nums[high]
        i=0
        for value1 in nums_copy:
            if value1==nums[low]:
                break
            ++i
        j=len(nums)-1
        for value2 in range(numSize-1,-1,-1):
            #倒序循环
            if value2==nums[high]:
                break
            --j
        return [i,j]
```
---












