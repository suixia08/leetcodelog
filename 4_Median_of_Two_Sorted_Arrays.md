# 二分法
>思路来自于---[公众号五分钟学算法](https://mp.weixin.qq.com/s/FBlH7o-ssj_iMEPLcvsY2w)
以及cnblogs--[Grandyang](https://www.cnblogs.com/grandyang/p/4465932.html)

>下面是我做的一些笔记，目前我也没有完全的理解此题，所以会有一些问题，欢迎在我的[博客](https://suixia.me)留言。
![LeetCode _4-1.jpg](https://i.loli.net/2019/09/01/HaBAL95TV2JSbsm.jpg)
![LeetCode _4-2.jpg](https://i.loli.net/2019/09/01/FYGb5VnqPHm9XzS.jpg)
![LeetCode _4-3.jpg](https://i.loli.net/2019/09/01/7n2NxYjmFidLDMy.jpg)

---
##### C++代码实现
```cpp
class Solution {
public:
  
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m=nums1.size();
        int n=nums2.size();
        //m,n分别表示两个数组的大小
        int k1=(m+n+1)/2;
        int k2=(m+n+2)/2;
        // k1,k2表示要找的第多少位数
        double ans1=findmid(nums1,0,nums2,0,k1);
        double ans2=findmid(nums1,0,nums2,0,k2);
        // ans1 ans2用于记录找到的两个数的大小
        return (ans1+ans2)/2;
    }
     //定义一个递归找数的函数，调用两次
     double findmid(vector<int>& nums1,int i,vector<int>& nums2,int j,int k)
     {
        //i,j用于保存被丢弃元素的个数，同时定位新的起点
         if(i==nums1.size())  
            return (double)nums2[j+k-1];
         /*第一种结束递归的条件：当num1中的数被丢弃完时，即要找的数不在num1中，此时只需在num2
         中直接可以找到所要找的数*/
        if(j==nums2.size())
            return (double)nums1[i+k-1];
         /*第二种结束递归的条件：当num2中的数被丢弃完时，即要找的数不在num2中，此时只需在num1
         中直接可以找到所要找的数*/
        if(k==1)
            return (double)min(nums1[i],nums2[j]);
         /*第三种结束递归的条件：要找的数是目前nums1[i]与nums2[j]中较小的一个，nums1[i]
         与nums2[j]表示目前两个数组除过被丢弃的数之外的第一个数*/
        
        /*
           midVal1与midVal2表示当前两个数组第k/2个数的大小，
           下面的代码为什么要这样写，是因为有一种特殊情况，
           就是可能某一个数组在当前递归层次中没有第K/2个数。
         */
         if(i+k/2>nums1.size())
              return findmid(nums1,i,nums2,j+k/2, k-k/2);
         else if(j+k/2>nums2.size())
              return findmid(nums1, i+k/2,nums2,j,k-k/2);
         //第k/2个数在两个数组都能找到的情况
         if(nums1[i+k/2-1]<nums2[j+k/2-1])
              return findmid(nums1, i+k/2,nums2,j,k-k/2);
         else  return findmid(nums1,i,nums2,j+k/2, k-k/2);
     }
};