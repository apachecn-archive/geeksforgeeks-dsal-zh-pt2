# C 程序计算 nPr 的值

> 原文:[https://www . geesforgeks . org/c-program-calculate-value-NPR/](https://www.geeksforgeeks.org/c-program-calculate-value-npr/)

nPr 代表 n [排列](http://en.wikipedia.org/wiki/Permutation) r，nPr 的值为(n！)/ (n-r)！。

## C

```
#include<stdio.h>

int fact(int n)
{
    if (n <= 1)
        return 1;
    return n*fact(n-1);
}

int nPr(int n, int r)
{
    return fact(n)/fact(n-r);
}

int main()
{
    int n, r;
    printf("Enter n: ");
    scanf("%d", &n);

    printf("Enter r: ");
    scanf("%d", &r);

    printf("%dP%d is %d", n, r, nPr(n, r));

    return 0;
}
```

```
Enter n: 5
Enter r: 2
5P2 is 20 
```

时间复杂度:0(n)

辅助空间:O(n)

计算 nPr 的有效方法请参考[排列系数](https://www.geeksforgeeks.org/permutation-coefficient/)。
如发现任何不正确的地方，请写评论，或者您想分享更多关于上述话题的信息