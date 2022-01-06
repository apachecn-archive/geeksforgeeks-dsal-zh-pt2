# 查找立方体对|集合 1(n^(2/3)解)

> 原文:[https://www . geesforgeks . org/find-cube-pairs-set-1-n23-solution/](https://www.geeksforgeeks.org/find-cube-pairs-set-1-n23-solution/)

给定一个数 n，找出两对可以表示该数为两个立方体之和的数。换句话说，找出两对(a，b)和(c，d)，这样给定的数 n 可以表示为

```
n = a^3 + b^3 = c^3 + d^3

```

其中 a、b、c 和 d 是四个不同的数字。

**示例:**

```
Input: N = 1729
Output: (1, 12) and (9, 10)
Explanation: 
1729 = 1^3 + 12^3 = 9^3 + 10^3

Input: N = 4104
Output: (2, 16) and (9, 15)
Explanation: 
4104 = 2^3 + 16^3 = 9^3 + 15^3

Input: N = 13832
Output: (2, 24) and (18, 20)
Explanation: 
13832 = 2^3 + 24^3 = 18^3 + 20^3

```

满足约束的任意数 n 将有两个不同的对(a，b)和(c，d)，使得 a，b，c 和 d 都小于 *n <sup>1/3</sup>* 。想法很简单。对于由小于 *n <sup>1/3</sup>* 的数字组成的每个不同对(x，y)，如果它们的和(x <sup>3</sup> + y <sup>3</sup> )等于给定的数字，我们使用和作为关键字将它们存储在哈希表中。如果总和等于给定数字的对再次出现，我们只需打印这两对。

```
1) Create an empty hash map, say s.
2) cubeRoot = n1/3
3) for (int x = 1; x < cubeRoot; x++)
     for (int y = x + 1; y <= cubeRoot; y++)
       int sum = x3 + y3;
       if (sum != n) continue;
       if sum exists in s,
         we found two pairs with sum, print the pairs
       else
         insert pair(x, y) in s using sum as key

```

以下是上述想法的实施–

## C++

```
// C++ program to find pairs that can represent
// the given number as sum of two cubes
#include <bits/stdc++.h>
using namespace std;

// Function to find pairs that can represent
// the given number as sum of two cubes
void findPairs(int n)
{
    // find cube root of n
    int cubeRoot = pow(n, 1.0/3.0);

    // create an empty map
    unordered_map<int, pair<int, int> > s;

    // Consider all pairs such with values less
    // than cuberoot
    for (int x = 1; x < cubeRoot; x++)
    {
        for (int y = x + 1; y <= cubeRoot; y++)
        {
            // find sum of current pair (x, y)
            int sum = x*x*x + y*y*y;

            // do nothing if sum is not equal to
            // given number
            if (sum != n)
                continue;

            // if sum is seen before, we found two pairs
            if (s.find(sum) != s.end())
            {
                cout << "(" << s[sum].first << ", "
                     << s[sum].second << ") and ("
                    << x << ", " << y << ")" << endl;
            }
            else
                // if sum is seen for the first time
                s[sum] = make_pair(x, y);
        }
    }
}

// Driver function
int main()
{
    int n = 13832;
    findPairs(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pairs that can represent
// the given number as sum of two cubes
import java.util.*;

class GFG
{
    static class pair
    {
        int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

// Function to find pairs that can represent
// the given number as sum of two cubes
static void findPairs(int n)
{
    // find cube root of n
    int cubeRoot = (int) Math.pow(n, 1.0/3.0);

    // create an empty map
    HashMap<Integer, pair> s = new HashMap<Integer, pair>();

    // Consider all pairs such with values less
    // than cuberoot
    for (int x = 1; x < cubeRoot; x++)
    {
        for (int y = x + 1; y <= cubeRoot; y++)
        {
            // find sum of current pair (x, y)
            int sum = x*x*x + y*y*y;

            // do nothing if sum is not equal to
            // given number
            if (sum != n)
                continue;

            // if sum is seen before, we found two pairs
            if (s.containsKey(sum))
            {
                System.out.print("(" + s.get(sum).first+ ", "
                    + s.get(sum).second+ ") and ("
                    + x+ ", " + y+ ")" +"\n");
            }
            else
                // if sum is seen for the first time
                s.put(sum, new pair(x, y));
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 13832;
    findPairs(n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find pairs
# that can represent the given
# number as sum of two cubes

# Function to find pairs that
# can represent the given number
# as sum of two cubes
def findPairs(n):

    # Find cube root of n
    cubeRoot = pow(n, 1.0 / 3.0);

    # Create an empty map
    s = {}

    # Consider all pairs such with
    # values less than cuberoot
    for x in range(int(cubeRoot)):
        for y in range(x + 1,
           int(cubeRoot) + 1):

            # Find sum of current pair (x, y)
            sum = x * x * x + y * y * y;

            # Do nothing if sum is not equal to
            # given number
            if (sum != n):
                continue;

            # If sum is seen before, we
            # found two pairs
            if sum in s.keys():
                print("(" + str(s[sum][0]) +
                     ", " + str(s[sum][1]) +
                        ") and (" + str(x) +
                             ", " + str(y) +
                              ")" + "\n")

            else:

                # If sum is seen for the first time
                s[sum] = [x, y]

# Driver code
if __name__=="__main__":

    n = 13832

    findPairs(n)

# This code is contributed by rutvik_56
```

## C#

```
// C# program to find pairs that can represent
// the given number as sum of two cubes
using System;
using System.Collections.Generic;

class GFG
{
    class pair
    {
        public int first, second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second;
        }
    }

// Function to find pairs that can represent
// the given number as sum of two cubes
static void findPairs(int n)
{
    // find cube root of n
    int cubeRoot = (int) Math.Pow(n, 1.0/3.0);

    // create an empty map
    Dictionary<int, pair> s = new Dictionary<int, pair>();

    // Consider all pairs such with values less
    // than cuberoot
    for (int x = 1; x < cubeRoot; x++)
    {
        for (int y = x + 1; y <= cubeRoot; y++)
        {
            // find sum of current pair (x, y)
            int sum = x*x*x + y*y*y;

            // do nothing if sum is not equal to
            // given number
            if (sum != n)
                continue;

            // if sum is seen before, we found two pairs
            if (s.ContainsKey(sum))
            {
                Console.Write("(" + s[sum].first+ ", "
                    + s[sum].second+ ") and ("
                    + x+ ", " + y+ ")" +"\n");
            }
            else
                // if sum is seen for the first time
                s.Add(sum, new pair(x, y));
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 13832;
    findPairs(n);
}
}

// This code is contributed by PrinciRaj1992
```

**输出:**

```
(2, 24) and (18, 20)

```

**上述解的时间复杂度**为 O(n <sup>2/3</sup> ，远小于 O(n)。

能否在 O(n <sup>1/3</sup> )时间内解决上述问题？我们将在下一篇文章中讨论这个问题。

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。