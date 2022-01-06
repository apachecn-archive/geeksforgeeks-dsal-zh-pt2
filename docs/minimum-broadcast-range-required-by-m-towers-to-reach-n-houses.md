# M 塔到达 N 栋房屋所需的最小广播范围

> 原文:[https://www . geesforgeks . org/m-towers-to-reach-n-houses 所需的最小广播范围/](https://www.geeksforgeeks.org/minimum-broadcast-range-required-by-m-towers-to-reach-n-houses/)

给定包含 **N 个房屋**的位置的阵列 **a** 和包含 **M 个无线电塔**的位置的阵列 **b** ，每个无线电塔沿着**水平线**放置，任务是找到最小广播范围，使得每个无线电塔到达每个房屋。
**举例:**

> **输入:** a[] = {1，5，11，20}，b[] = {4，8，15}
> **输出:** 5
> **解释:**
> 所需的最小范围是 5，因为这将是 15 号位置的塔到达 20 号位置的房子所需要的
> **输入:** a[] = {12，13，11，80}，b[] = {4，6，15

**方法:**遍历两个数组，直到计算出最后一个房子的广播范围。对于每栋房子，分别比较它与左右塔楼的距离，考虑最小值。将该最小值与目前获得的最大值进行比较，并存储最大值。
**注:**左塔距首宅的距离考虑 [**整数。最小值**](https://www.geeksforgeeks.org/integer-max_value-and-integer-min_value-in-java-with-examples/) 。如果我们到达塔的末端，所有剩余房屋与相应右塔的距离被认为是 [**整数。MAX_VALUE**](https://www.geeksforgeeks.org/integer-max_value-and-integer-min_value-in-java-with-examples/) 。
下面的代码实现了上面的方法:

## C++

```
// CPP program to implement the above approach
#include<bits/stdc++.h>
using namespace std;

int minBroadcastRange(int houses[], int towers[],int n,int m)
    {
        // Initialize distance of left
        // tower from first house
        int leftTower = INT_MIN;

        // Initialize distance of right
        // tower from first house
        int rightTower = towers[0];

        // j: Index of houses[]
        // k: Index of towers[]
        int j = 0, k = 0;

        // Store the minimum required range
        int min_range = 0;

        while (j < n) {

            // If the house lies between
            // left and right towers
            if (houses[j] < rightTower) {

                int left = houses[j] - leftTower;
                int right = rightTower - houses[j];

                // Compare the distance between the
                // left and right nearest towers
                int local_max = left < right ? left : right;

                if (local_max > min_range)

                    // updating the maximum value
                    min_range = local_max;
                j++;
            }
            else {

                // updating the left tower
                leftTower = towers[k];

                if (k < m - 1) {

                    k++;
                    // updating the right tower
                    rightTower = towers[k];
                }
                else
                    // updating right tower
                    // to maximum value after
                    // reaching the end of Tower array
                    rightTower = INT_MAX;
            }
        }
        return min_range;
    }

    // Driver code
    int main()
    {
        int a[] = { 12, 13, 11, 80 };
        int b[] = { 4, 6, 15, 60 };
        int n = sizeof(a)/sizeof(a[0]);
        int m = sizeof(b)/sizeof(b[0]);
        int max = minBroadcastRange(a, b,n,m);
        cout<<max<<endl;
    }

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach

import java.io.*;

class GFG {

    private static int minBroadcastRange(
        int[] houses, int[] towers)
    {

        // Store no of houses
        int n = houses.length;

        // Store no of towers
        int m = towers.length;

        // Initialize distance of left
        // tower from first house
        int leftTower = Integer.MIN_VALUE;

        // Initialize distance of right
        // tower from first house
        int rightTower = towers[0];

        // j: Index of houses[]
        // k: Index of towers[]
        int j = 0, k = 0;

        // Store the minimum required range
        int min_range = 0;

        while (j < n) {

            // If the house lies between
            // left and right towers
            if (houses[j] < rightTower) {

                int left = houses[j] - leftTower;
                int right = rightTower - houses[j];

                // Compare the distance between the
                // left and right nearest towers
                int local_max = left < right ? left : right;

                if (local_max > min_range)

                    // updating the maximum value
                    min_range = local_max;
                j++;
            }
            else {

                // updating the left tower
                leftTower = towers[k];

                if (k < m - 1) {

                    k++;
                    // updating the right tower
                    rightTower = towers[k];
                }
                else
                    // updating right tower
                    // to maximum value after
                    // reaching the end of Tower array
                    rightTower = Integer.MAX_VALUE;
            }
        }
        return min_range;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 12, 13, 11, 80 };
        int[] b = { 4, 6, 15, 60 };
        int max = minBroadcastRange(a, b);
        System.out.println(max);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to implement the above approach
import sys

def minBroadcastRange( houses, towers, n, m):

    # Initialize distance of left
    # tower from first house
    leftTower = -sys.maxsize - 1

    # Initialize distance of right
    # tower from first house
    rightTower = towers[0]

    # j: Index of houses[]
    # k: Index of towers[]
    j , k = 0 , 0

    # Store the minimum required range
    min_range = 0

    while (j < n):

        # If the house lies between
        # left and right towers
        if (houses[j] < rightTower):

            left = houses[j] - leftTower
            right = rightTower - houses[j]

            # Compare the distance between the
            # left and right nearest towers
            if left < right :
                local_max = left
            else:
                local_max = right

            if (local_max > min_range):

                # updating the maximum value
                min_range = local_max
            j += 1

        else:

            # updating the left tower
            leftTower = towers[k]

            if (k < m - 1) :

                k += 1

                # updating the right tower
                rightTower = towers[k]

            else:
                # updating right tower
                # to maximum value after
                # reaching the end of Tower array
                rightTower = sys.maxsize
    return min_range

# Driver code
if __name__ == "__main__":

    a = [ 12, 13, 11, 80 ]
    b = [ 4, 6, 15, 60 ]
    n = len(a)
    m = len(b)
    max = minBroadcastRange(a, b,n,m)
    print(max)

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement the above approach
 using System;

class GFG {

    private static int minBroadcastRange(
        int[] houses, int[] towers)
    {

        // Store no of houses
        int n = houses.Length;

        // Store no of towers
        int m = towers.Length;

        // Initialize distance of left
        // tower from first house
        int leftTower = int.MinValue;

        // Initialize distance of right
        // tower from first house
        int rightTower = towers[0];

        // j: Index of houses[]
        // k: Index of towers[]
        int j = 0, k = 0;

        // Store the minimum required range
        int min_range = 0;

        while (j < n) {

            // If the house lies between
            // left and right towers
            if (houses[j] < rightTower) {

                int left = houses[j] - leftTower;
                int right = rightTower - houses[j];

                // Compare the distance between the
                // left and right nearest towers
                int local_max = left < right ? left : right;

                if (local_max > min_range)

                    // updating the maximum value
                    min_range = local_max;
                j++;
            }
            else {

                // updating the left tower
                leftTower = towers[k];

                if (k < m - 1) {

                    k++;
                    // updating the right tower
                    rightTower = towers[k];
                }
                else
                    // updating right tower
                    // to maximum value after
                    // reaching the end of Tower array
                    rightTower = int.MaxValue;
            }
        }
        return min_range;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] a = { 12, 13, 11, 80 };
        int[] b = { 4, 6, 15, 60 };
        int max = minBroadcastRange(a, b);
        Console.WriteLine(max);
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

function minBroadcastRange(
       houses, towers)
    {

        // Store no of houses
        let n = houses.length;

        // Store no of towers
        let m = towers.length;

        // Initialize distance of left
        // tower from first house
        let leftTower = Number.MIN_VALUE;

        // Initialize distance of right
        // tower from first house
        let rightTower = towers[0];

        // j: Index of houses[]
        // k: Index of towers[]
        let j = 0, k = 0;

        // Store the minimum required range
        let min_range = 0;

        while (j < n) {

            // If the house lies between
            // left and right towers
            if (houses[j] < rightTower) {

                let left = houses[j] - leftTower;
                let right = rightTower - houses[j];

                // Compare the distance between the
                // left and right nearest towers
                let local_max = left < right ? left : right;

                if (local_max > min_range)

                    // updating the maximum value
                    min_range = local_max;
                j++;
            }
            else {

                // updating the left tower
                leftTower = towers[k];

                if (k < m - 1) {

                    k++;
                    // updating the right tower
                    rightTower = towers[k];
                }
                else
                    // updating right tower
                    // to maximum value after
                    // reaching the end of Tower array
                    rightTower = Number.MAX_VALUE;
            }
        }
        return min_range;
    }

// Driver Code

        let a = [12, 13, 11, 80 ];
        let b = [ 4, 6, 15, 60 ];
        let max = minBroadcastRange(a, b);
        document.write(max);

</script>
```

**Output:** 

```
20
```

***时间复杂度:** O(M + N)*

***辅助空间:**O(1)*T4】