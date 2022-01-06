# 范围[L，R]

内的整数计数(2^x * 3^y)

> 原文:[https://www . geesforgeks . org/整数形式计数-2x-3y 范围内-l-r/](https://www.geeksforgeeks.org/count-of-integers-of-the-form-2x-3y-in-the-range-l-r/)

给定一个范围**【L，R】**，其中**0≤L≤R≤10<sup>8</sup>T5。任务是从给定范围内找出可以表示为**(2<sup>x</sup>)*(3<sup>y</sup>)**的整数个数。
**示例:**** 

> **输入:** L = 1，R = 10
> **输出:** 7
> 数字为 1、2、3、4、6、8 和 9
> **输入:** L = 100，R = 200
> **输出:** 5
> 数字为 108、128、144、162 和 192

**逼近:**由于数字是 2 和 3 的幂，增长很快，可以使用以下算法。对于**(2<sup>x</sup>)*(3<sup>y</sup>)**范围内**【1，10<sup>8</sup>**的所有数字，将其存储在一个向量中。稍后对向量进行排序。然后可以使用[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)计算所需答案。当有多个**【L，R】**形式的查询时，预先计算这些整数会有帮助。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define MAXI (int)(1e8)

// To store all valid integers
vector<int> v;

// Function to find all the integers of the
// form (2^x * 3^y) in the range [0, 1000000]
void precompute()
{

    // To store powers of 2 and 3
    // initialized to 2^0 and 3^0
    int x = 1, y = 1;

    // While current power of 2
    // is within the range
    while (x <= MAXI) {

        // While number is within the range
        while (x * y <= MAXI) {

            // Add the number to the vector
            v.push_back(x * y);

            // Next power of 3
            y *= 3;
        }

        // Next power of 2
        x *= 2;

        // Reset to 3^0
        y = 1;
    }

    // Sort the vector
    sort(v.begin(), v.end());
}

// Function to find the count of numbers
// in the range [l, r] which are
// of the form (2^x * 3^y)
void countNum(int l, int r)
{
    cout << upper_bound(v.begin(), v.end(), r)
                - upper_bound(v.begin(), v.end(), l - 1);
}

// Driver code
int main()
{
    int l = 100, r = 200;

    // Pre-compute all the valid numbers
    precompute();

    countNum(l, r);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import bisect
MAXI=int(1e8)

# To store all valid integers
v=[]

# Function to find all the integers of the
# form (2^x * 3^y) in the range [0, 1000000]
def precompute():

    # To store powers of 2 and 3
    # initialized to 2^0 and 3^0
    x = 1; y = 1

    # While current power of 2
    # is within the range
    while (x <= MAXI) :

        # While number is within the range
        while (x * y <= MAXI) :

            # Add the number to the vector
            v.append(x * y)

            # Next power of 3
            y *= 3

        # Next power of 2
        x *= 2

        # Reset to 3^0
        y = 1

    # Sort the vector
    v.sort()

# Function to find the count of numbers
# in the range [l, r] which are
# of the form (2^x * 3^y)
def countNum(l, r):
    print(bisect.bisect_right(v, r) - bisect.bisect_right(v,l - 1))

# Driver code
if __name__ == '__main__':
    l = 100; r = 200

    # Pre-compute all the valid numbers
    precompute()

    countNum(l, r)
```

**Output:** 

```
5
```

**时间复杂度:** O(N * log(N))，其中 N = logX+logY
T3】辅助空间: O(N)