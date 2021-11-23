```c++

// 最长递增子序列
// dp[i]的含义是 以第i个元素结尾的最长递增子串的长度

# include <algorithm>
int lengthOfLIS(vector<int> &nums)
{
    int n = (int)nums.size();
    // 设置边界条件
    if (n == 0)
    {
        return 0;
    }
    // 优雅的初始化
    vector<int> dp(n, 0);
    for (int i = 0; i < n; i++)
    {
        // 让每一个dp都初始化为1，因为这是一定的。这句删掉就报错！！！！
        dp[i] = 1;
        for (int j = 0; j < i; j++)
        {

            if (nums[i] > nums[j])
                // 还要比一下自己 这是为什么呢？
                dp[i] = max(dp[i], dp[j] + 1);
        }
    }
    return *max_element(dp.begin(), dp.end());
}
```

