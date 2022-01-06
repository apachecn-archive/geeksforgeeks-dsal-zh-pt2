# 平面平行四边形的计数

> 原文:[https://www.geeksforgeeks.org/count-parallelograms-plane/](https://www.geeksforgeeks.org/count-parallelograms-plane/)

给定平面上的一些点，这些点是不同的，并且没有三个点位于同一条线上。我们需要找到以顶点为给定点的平行四边形的数目。
示例:

```
Input : points[] = {(0, 0), (0, 2), (2, 2), (4, 2), 
                                   (1, 4), (3, 4)}
Output : 2
Two Parallelograms are possible by choosing above
given point as vertices, which are shown in below 
diagram.

```

我们可以利用平行四边形的一个特殊性质来解决这个问题，即平行四边形的对角线在中间相交。所以如果我们得到这样一个中间点，它是一个以上线段的中间点，那么我们可以得出平行四边形存在的结论，更准确地说，如果一个中间点出现 x 次，那么可能的平行四边形的对角线可以通过 <sup>x</sup> C <sub>2</sub> 的方式来选择，即会有 x*(x-1)/2 个平行四边形对应于这个特定的中间点，频率为 x。所以我们迭代所有的点对，我们计算它们的中间点，并将中间点的频率增加 1。最后，如上所述，我们根据每个不同中间点的频率计算平行四边形的数量。由于我们只需要中间点的频率，为了简单起见，在计算中间点时忽略了除以 2。

```
// C++ program to get number of Parallelograms we
// can make by given points of the plane
#include <bits/stdc++.h>
using namespace std;

// Returns count of Parallelograms possible
// from given points
int countOfParallelograms(int x[], int y[], int N)
{
    // Map to store frequency of mid points
    map<pair<int, int>, int> cnt;
    for (int i=0; i<N; i++)
    {
        for (int j=i+1; j<N; j++)
        {
            // division by 2 is ignored, to get
            // rid of doubles
            int midX = x[i] + x[j];
            int midY = y[i] + y[j];

            // increase the frequency of mid point
            cnt[make_pair(midX, midY)]++;
        }
    }

    // Iterating through all mid points
    int res = 0;
    for (auto it = cnt.begin(); it != cnt.end(); it++)
    {
        int freq = it->second;

        // Increase the count of Parallelograms by
        // applying function on frequency of mid point
        res += freq*(freq - 1)/2
    }

    return res;
}

//  Driver code to test above methods
int main()
{
    int x[] = {0, 0, 2, 4, 1, 3};
    int y[] = {0, 2, 2, 2, 4, 4};
    int N = sizeof(x) / sizeof(int);

    cout << countOfParallelograms(x, y, N) << endl;

    return 0;
}
```

输出:

```
2

```

本文由 **[乌卡什·特里维迪](https://in.linkedin.com/in/utkarsh-trivedi-253069a7)** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。