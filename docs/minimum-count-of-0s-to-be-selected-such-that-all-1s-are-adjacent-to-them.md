# 选择 0 的最小计数，使所有 1 都与其相邻

> 原文:[https://www . geesforgeks . org/待选 0 的最小计数-这样所有 1 都与它们相邻/](https://www.geeksforgeeks.org/minimum-count-of-0s-to-be-selected-such-that-all-1s-are-adjacent-to-them/)

给定一个大小为 **N** 的二进制字符串 **str** ，其每个字符要么是**“1”**要么是**“0”**。任务是选择 **0** 的**最小**数量，以便每**“1”**至少选择一个邻居。打印所选**0′**s 的**计数**。

**示例:**

> **输入:** str = "1001"
> **输出:** 2
> **说明:**0 可以从索引 1 和索引 2 中选择。因此，每个“1”在选定的“0”中至少有一个“T8”邻居
> 
> **输入:** str = "01010"
> **输出** : 1
> **说明:**可以选择索引 2 处的‘0’。结果，两个 1 的一个邻居被选择。
> 
> **输入:** str = "111"
> **输出:** -1
> **说明:**给定字符串中没有‘0’。因此“1”的任何邻居都不能是“0”。
> 
> **输入:** str = "110"
> **输出:** -1
> **说明:**第一个位置没有‘0’作为‘1’的邻居。

**进场:**解决方案基于 [**贪婪**](http://www.geeksforgeeks.org/greedy-algorithms/) 进场。按照以下步骤获得解决方案。

*   开始从头开始迭代字符串。
*   如果可能，为每个“1”从其邻域中选择一个“0”。
*   现在，如果在电流**【1】**之前和之后都有**【0】****，那么总是选择电流**【1】旁边的邻居**(因为在这个之后可以有更多的“1”，这样做将允许选择最小数量的邻居)。**

下面是上述方法的实现:

## C++

```
// C++ code to implememnt the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count
// minimum number of buckets
int minimumBuckets(string str)
{
    int bucketcount = 0;
    int N = str.size();

    // Loop to count minimum buckets
    for (int i = 0; i < N;) {
        if (str[i] == '1') {

            // If bucket can be put,
            // no need of next two indices,
            // so shift to i+3
            if (i + 1 < N &&
                str[i + 1] == '0') {
                bucketcount++;
                i += 3;
                continue;
            }
            if (i - 1 >= 0 &&
                str[i - 1] == '0') {
                bucketcount++;
                i++;
                continue;
            }
            return -1;
        }
        i++;
    }
    return bucketcount;
}

// Driver code
int main()
{
    string str = "1001";
    cout << minimumBuckets(str)<<endl;

    string str1 = "1010";
    cout << minimumBuckets(str1);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implememnt the above approach
class GFG {

    // Function to count
    // minimum number of buckets
    static int minimumBuckets(String str) {
        int bucketcount = 0;
        int N = str.length();

        // Loop to count minimum buckets
        for (int i = 0; i < N;) {
            if (str.charAt(i) == '1') {

                // If bucket can be put,
                // no need of next two indices,
                // so shift to i+3
                if (i + 1 < N && str.charAt(i + 1) == '0') {
                    bucketcount++;
                    i += 3;
                    continue;
                }
                if (i - 1 >= 0 && str.charAt(i - 1) == '0') {
                    bucketcount++;
                    i++;
                    continue;
                }
                return -1;
            }
            i++;
        }
        return bucketcount;
    }

    // Driver code
    public static void main(String args[]) {
        String str = "1001";
        System.out.println(minimumBuckets(str));

        String str1 = "1010";
        System.out.println(minimumBuckets(str1));
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# python code to implememnt the above approach

# Function to count
# minimum number of buckets
def minimumBuckets(str):

    bucketcount = 0
    N = len(str)

    # Loop to count minimum buckets
    i = 0
    while(i < N):
        if (str[i] == '1'):

            # If bucket can be put,
            # no need of next two indices,
            # so shift to i+3
            if (i + 1 < N and str[i + 1] == '0'):
                bucketcount += 1
                i += 3
                continue

            if (i - 1 >= 0 and str[i - 1] == '0'):
                bucketcount += 1
                i += 1
                continue

            return -1

        i += 1

    return bucketcount

# Driver code
if __name__ == "__main__":

    str = "1001"
    print(minimumBuckets(str))

    str1 = "1010"
    print(minimumBuckets(str1))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code to implememnt the above approach
using System;
class GFG {

    // Function to count
    // minimum number of buckets
    static int minimumBuckets(string str)
    {
        int bucketcount = 0;
        int N = str.Length;

        // Loop to count minimum buckets
        for (int i = 0; i < N;) {
            if (str[i] == '1') {

                // If bucket can be put,
                // no need of next two indices,
                // so shift to i+3
                if (i + 1 < N && str[i + 1] == '0') {
                    bucketcount++;
                    i += 3;
                    continue;
                }
                if (i - 1 >= 0 && str[i - 1] == '0') {
                    bucketcount++;
                    i++;
                    continue;
                }
                return -1;
            }
            i++;
        }
        return bucketcount;
    }

    // Driver code
    public static void Main()
    {
        string str = "1001";
        Console.WriteLine(minimumBuckets(str));

        string str1 = "1010";
        Console.WriteLine(minimumBuckets(str1));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript code for the above approach

        // Function to count
        // minimum number of buckets
        function minimumBuckets(str) {
            let bucketcount = 0;
            let N = str.length;

            // Loop to count minimum buckets
            for (let i = 0; i < N;) {
                if (str[i] == '1') {

                    // If bucket can be put,
                    // no need of next two indices,
                    // so shift to i+3
                    if (i + 1 < N &&
                        str[i + 1] == '0') {
                        bucketcount++;
                        i += 3;
                        continue;
                    }
                    if (i - 1 >= 0 &&
                        str[i - 1] == '0') {
                        bucketcount++;
                        i++;
                        continue;
                    }
                    return -1;
                }
                i++;
            }
            return bucketcount;
        }

        // Driver code
        let str = "1001";
        document.write(minimumBuckets(str) + '<br>');

        let str1 = "1010";
        document.write(minimumBuckets(str1) + '<br>');

  // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
1
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)