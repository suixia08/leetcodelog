# 3  Longest Substring Without Repeating Characters
### 1.暴力解法
>具体思路大概是设置一个256大小的数组，用于表示全部的ASCII码，初始化为0，从第一个字符开始循环遍历，遇到哪一个字符就将对应的数组元素自增，然后判断是否等于2，如果等于2，就将当前遍历所得的最大不重复字串字符数与表示最大长度的max进行比较，如果大于max,就将max赋值为当前遍历的最大值，然后从第二个字符进行遍历，重复上述操作，直到结束。
##### C++
```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int arr[256]={0};
        int len=s.length();
        int max=0;
        int count=0;
        int j=0;
        while(j<len)
        {
        for(int i=j;i<len;i++)
        {
            int m=s[i];
            arr[m]++; 
            if(arr[m]!=2)
            {
                count++;
                if(count>max)
                    max=count;
            }
            else 
            {
                for(int k=0;k<256;k++)
                    arr[k]=0;
                count=0;
                break;
            }
        }
            j++;
        }
        return max;
    }
};