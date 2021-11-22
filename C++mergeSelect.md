``` c++
#include <stdio.h>
#include <iostream>
using namespace std;
#define ARR_LEN(array, length)                     \
    {                                              \
        length = sizeof(array) / sizeof(array[0]); \
    }

#define ARR_LEN 这是一种常用的C++数组长度求法的定义式


# 交换
void swap(int a, int b)
{
    int temp = a;
    a = b;
    b = temp;
}

#我愿称之为分组
int partition(int a[], int p, int r)
{
    #定义头位置
    int i = p;
    #定位不存在的尾位置
    int j = r + 1;
    # 将头位置元素设为分割元素
    int x = a[i];
    
    while (1)
    {
        # 一直向前推进，直到找到一个比x大的元素 卡住。
        while (a[++i] < x && i < r)
            ;
		# 一直向后推进，直到找到一个比x小的元素 卡住。
        while (a[--j] > x && j > p)
            ;
        # 如果j比i小了，说明推进完了，直接退出。
        if (j <= i)
            break;
       	# 交换这两个数的位置
        int temp = a[j];
        a[j] = a[i];
        a[i] = temp;
    }
    # 最后这里，初始位置用最后j在位置定位
    a[p] = a[j];
    # a[j]的位置则由x即分割元素定位
    a[j] = x;
    # 返回分割元素的位置
    return j;
}

int MergeSelect(int a[], int p, int r, int k)
{
    if (p == r)
        return a[p];
    int ind = partition(a, p, r);
    # j为前半部包括分割元素的长度。
    int j = ind - p + 1;
    if (j >= k)
    {
        return MergeSelect(a, p, ind, k);
    }
    else
    {
        return MergeSelect(a, ind + 1, r, k - j);
    }
}

void disp(int *a,int length)
{
    for (int i = 0; i < length; i++)
    {
        cout << a[i]<<' ';
    }
}

int main()
{
    int a[] = {5, 2, 0, 7, 3, 4};
    int len;
    ARR_LEN(a, len);
    int ind = partition(a, 0, len - 1);
    disp(a,len);
    return 0;
}
```

