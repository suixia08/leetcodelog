# 7 Reverse Integer
>当给定的X非常大或者非常小的时候，就要考虑溢出的问题，因为32位有符号整数的取值范围是-2147483648——2147483647，所以当除模运算到最高位的时候要判断rev*10有没有超过上下界，如果刚好等于上下界，则要判断最后一个除模运算后的数是否小于-8或者大于7。

### c++
```cpp
class Solution {
public:
    int reverse(int x) {
        int temp;
        int rev=0;
        while(x!=0)
        {
            temp=x%10;
            x/=10;
            //这里要考虑溢出的情况
            if(rev>INT_MAX/10 || (rev==INT_MAX/10 && temp>7))
                return 0;
            if(rev<INT_MIN/10 || (rev==INT_MIN/10 && temp<-8))
                return 0;
            rev=rev*10+temp;  
        }
        return rev;
    }
};
