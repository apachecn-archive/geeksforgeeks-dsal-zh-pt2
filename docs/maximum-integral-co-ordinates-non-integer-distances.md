# 非整数距离的最大积分坐标

> 原文:[https://www . geesforgeks . org/maximum-integral-co-coordinates-non-integer-distance/](https://www.geeksforgeeks.org/maximum-integral-co-ordinates-non-integer-distances/)

给定 x 坐标和 y 坐标的最大限制，我们希望计算一组坐标，使得任意两点之间的距离为非整数。选择的坐标(I，j)应该在 0<=i<=x 和 0<=j<=y 的范围内。此外，我们必须最大化集合。

示例:

```
Input : 4 4
Output : 0 4
         1 3
         2 2
         3 1
         4 0
Explanation : Distance between any two points
mentioned in output is not integer.
```

首先，我们想创建一个集合，这意味着我们的集合不能包含任何其他与之前使用的 x 或 y 相同的点。这背后的原因是，这些点要么有相同的 x 坐标，要么有相同的 y 坐标，它们会抵消这个坐标，导致它们之间有一个积分距离。
例如，考虑点(1，4)和(1，5)，x 坐标将取消，因此，我们将获得和积分距离。
其次，我们可以观察到，我们只有 x+1 个不同的 I 坐标和 y+1 个不同的 j 坐标。因此，集合的大小不能超过 min(x，y)+1。
第三个观察是，我们知道对角元素相距|i-j|* ![sqrt(2)    ](img/aa44ef91d9f189fd913ac56aeb015f25.png "Rendered by QuickLaTeX.com")距离，因此，我们取沿 I-坐标的对角元素求值，并通过公式 min(i，j)-i 计算 j-坐标

## C++

```
// C++ program to find maximum integral points
// such that distances between any two is not
// integer.
#include <bits/stdc++.h>
using namespace std;

// Making set of coordinates such that
// any two points are non-integral distance apart
void printSet(int x, int y)
{
    // used to avoid duplicates in result
    set<pair<int, int> > arr;

    for (int i = 0; i <= min(x, y); i++) {

        pair<int, int> pq;
        pq = make_pair(i, min(x, y) - i);
        arr.insert(pq);
    }

    for (auto it = arr.begin(); it != arr.end(); it++)
        cout << (*it).first << " " << (*it).second << endl;
}

// Driver function
int main()
{
    int x = 4, y = 4;
    printSet(x, y);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find maximum integral points
# such that distances between any two is not
# integer.

# Making set of coordinates such that
# any two points are non-integral distance apart
def printSet(x, y):

    # Used to avoid duplicates in result
    arr = []

    for i in range(min(x, y) + 1):
        pq = [i, min(x, y) - i]
        arr.append(pq)

    for it in arr:
        print(it[0], it[1])

# Driver code
if __name__ == "__main__":

    x = 4
    y = 4

    printSet(x, y)

# This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program to find maximum integral points
// such that distances between any two is not
// integer.

    // Making set of coordinates such that
// any two points are non-integral distance apart
    function printSet(x,y)
    {
    // used to avoid duplicates in result
        arr=[];
        for (let i = 0; i <= Math.min(x, y); i++)
        {
            let pq = [i, Math.min(x, y) - i];
            arr.push(pq);
        }
       // document.write(arr);
        for (let [key,value] of arr.entries())
        {
            document.write(value[0]+" "+value[1]+"<br>")
        }
    }

    // Driver function
    let x = 4;
    let y = 4;
    printSet(x, y)

    // This code is contributed by rag2127

</script>
```

**输出:**

```
0 4
1 3
2 2
3 1
4 0
```