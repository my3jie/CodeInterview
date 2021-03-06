## 题目描述

HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)

## 解题思路

假设数组[a, b, c, d, e, f],如果a+b+c < c,则a和b就没有被当作最大连续和的必要了。直接从c开始计算新的最大连续和就行了。

## C++代码
```
class Solution {
public:
    int FindGreatestSumOfSubArray(vector<int> array) {
        int greatest = INT_MIN;        

        int sum = 0;
        for(auto x : array)
        {
            //[1,-2,3,10,-4, 7, 2,-5]
            //[-2,-8,-1,-5,-9]
            //[a, b, c, d]
            if(sum < 0)
                sum = x;
            else
                sum += x;

            if(sum > greatest)
                greatest = sum;
        }

        return greatest;
    }
};
```

## 易错点
太纠结于什么时候去保存最大sum了，其实每次循环一次就进行比较并且保存最大和，是最简单的方案。