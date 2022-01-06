# 找到一个点，该点与一条线上所有给定点的距离之和为 K

> 原文:[https://www . geeksforgeeks . org/find-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-a-](https://www.geeksforgeeks.org/find-a-point-whose-sum-of-distances-from-all-given-points-on-a-line-is-k/)

给定一个排序的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**由 **N** 个整数组成，代表一条线上的点和一个整数 **K** ，任务是找到第一个点和最后一个点之间的任意点 **P** ，使得所有给定点到 **P** 的距离之和等于 **K** 。如果不存在这样的点，则打印**-1”**。

**示例:**

> **输入:** arr[] = {1，3，6，7，11}，K = 18
> **输出:** 8
> **说明:**
> 把 P 的值考虑为 8。因此，P(= 8)与所有点的距离之和为(8–1)+(8–3)+(8–6)+(8–7)+(11–8)= 18(= K)，等于给定值 K，点 8 位于第一个(= 1)点和最后一个(= 11)点之间。
> 
> **输入:** arr[] = {-10，-2，1，2}，K = 29
> T3】输出: -9

**方法:**给定的问题可以基于这样的观察来解决，即距离之和在阵列的[中间值](https://www.geeksforgeeks.org/median/)处最小，并且当从中间值向任意末端移动时，距离增加。因此，想法是在阵列的两半上执行[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，并检查是否有任何点的距离等于 **K** 。按照以下步骤解决问题:

*   声明一个函数，该函数计算所有点到给定点的距离之和。
*   在数组的右半部分执行一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)如下:
    *   如果 **N** 的值为奇数，则更新**左**的值为**arr【N/2】**。否则，将左侧**的值更新为**arr【N/2–1】+1**。**
    *   **如果 **N** 的值为偶数，则将**右**的值更新为**arr【N–1】**。**
    *   **求从**中间=(左+右)/ 2** 的距离之和 **temp** ，检查 **temp** 的值是否等于 **K** 。如果发现**为真**，则打印**中间**的值作为结果。**
    *   **如果 **K < temp** 的值，则更新**右**的值为**中-1**。否则，将左侧**的值更新为**中间+ 1** 。****
*   ****在阵列的左半部分执行二分搜索法操作:

    *   设置**左= arr[0]** 和**右= arr[N/2]–1**的值。
    *   求从**中间=(左+右)/ 2** 到**温度**的距离之和**温度**是否等于 **K** 。如果发现**为真**，则打印**中间**的值作为结果。
    *   如果 **K > temp** 的值，则更新**right = mid–1**的值。否则，更新**左=中+ 1** 的值。**** 
*   ****如果在左半部分和右半部分没有找到值，则打印**-1”**作为结果。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of distances
// of all points from a given point
int findSum(int* arr, int N, int pt)
{
    // Stores sum of distances
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        sum += abs(arr[i] - pt);
    }

    // Return the sum
    return sum;
}

// Function to find such a point having
// sum of distances of all other points
// from this point equal to K
void findPoint(int* arr, int N, int K)
{
    // If N is odd keep left as arr[n / 2]
    // else keep left as arr[n / 2 - 1] + 1;
    int left;

    if (N % 2) {
        left = arr[N / 2];
    }
    else {
        left = arr[N / 2 - 1] + 1;
    }

    // Keep right as arr[N - 1]
    int right = arr[N - 1];

    // Perform binary search in the
    // right half
    while (left <= right) {

        // Calculate the mid index
        // of the range
        int mid = (left + right) / 2;

        int temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K) {

            // Print the value of mid
            cout << mid << endl;
            return;
        }

        // If the value of K < temp
        else if (K < temp) {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If the value of K > temp
        else {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // Update the value of left
    left = arr[0];

    // Update the value of right
    right = arr[N / 2] - 1;

    // Perform binary search on the
    // left half
    while (left <= right) {

        // Calculate the mid index
        // of the range
        int mid = (left + right) / 2;

        int temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K) {

            // Print mid
            cout << mid << endl;
            return;
        }

        // if K > temp
        else if (K > temp) {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If K < temp
        else {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // If no such point found
    cout << "-1" << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 6, 7, 11 };
    int K = 18;
    int N = sizeof(arr) / sizeof(arr[0]);
    findPoint(arr, N, K);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.lang.*;

class GFG{

// Function to find the sum of distances
// of all points from a given point
public static int findSum(int arr[], int N,
                          int pt)
{

    // Stores sum of distances
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        sum += Math.abs(arr[i] - pt);
    }

    // Return the sum
    return sum;
}

// Function to find such a point having
// sum of distances of all other points
// from this point equal to K
public static void findPoint(int arr[], int N, int K)
{

    // If N is odd keep left as arr[n / 2]
    // else keep left as arr[n / 2 - 1] + 1;
    int left;

    if (N % 2 != 0)
    {
        left = arr[N / 2];
    }
    else
    {
        left = arr[N / 2 - 1] + 1;
    }

    // Keep right as arr[N - 1]
    int right = arr[N - 1];

    // Perform binary search in the
    // right half
    while (left <= right)
    {

        // Calculate the mid index
        // of the range
        int mid = (left + right) / 2;

        int temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K)
        {

            // Print the value of mid
            System.out.println(mid);
            return;
        }

        // If the value of K < temp
        else if (K < temp)
        {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If the value of K > temp
        else
        {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // Update the value of left
    left = arr[0];

    // Update the value of right
    right = arr[N / 2] - 1;

    // Perform binary search on the
    // left half
    while (left <= right)
    {

        // Calculate the mid index
        // of the range
        int mid = (left + right) / 2;

        int temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K)
        {

            // Print mid
            System.out.println(mid);
            return;
        }

        // if K > temp
        else if (K > temp)
        {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If K < temp
        else
        {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // If no such point found
    System.out.println( "-1" );
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 3, 6, 7, 11 };
    int K = 18;
    int N = arr.length;

    findPoint(arr, N, K);
}
}

// This code is contributed by SoumikMondal**
```

## ****蟒蛇 3****

```
**# python 3 program for the above approach

# Function to find the sum of distances
# of all points from a given point
def findSum(arr, N, pt):

    # Stores sum of distances
    sum = 0

    # Traverse the array
    for i in range(N):
        sum += abs(arr[i] - pt)

    # Return the sum
    return sum

# Function to find such a point having
# sum of distances of all other points
# from this point equal to K
def findPoint(arr, N, K):
    # If N is odd keep left as arr[n / 2]
    # else keep left as arr[n / 2 - 1] + 1;
    left = 0

    if (N % 2):
        left = arr[N // 2]
    else:
        left = arr[N // 2 - 1] + 1

    # Keep right as arr[N - 1]
    right = arr[N - 1]

    # Perform binary search in the
    # right half
    while (left <= right):

        # Calculate the mid index
        # of the range
        mid = (left + right) // 2

        temp = findSum(arr, N, mid)

        # If temp is equal to K
        if (temp == K):
            # Print the value of mid
            print(mid)
            return

        # If the value of K < temp
        elif (K < temp):
            # Update right to mid - 1
            right = mid - 1

        # If the value of K > temp
        else:
            # Update left to mid + 1
            left = mid + 1

    # Update the value of left
    left = arr[0]

    # Update the value of right
    right = arr[N // 2] - 1

    # Perform binary search on the
    # left half
    while (left <= right):
        # Calculate the mid index
        # of the range
        mid = (left + right) // 2

        temp = findSum(arr, N, mid)

        # If temp is equal to K
        if (temp == K):

            # Print mid
            print(mid)
            return

        # if K > temp
        elif(K > temp):
            # Update right to mid - 1
            right = mid - 1

        # If K < temp
        else:
            # Update left to mid + 1
            left = mid + 1

    # If no such point found
    print("-1")

# Driver Code
if __name__ == '__main__':
    arr = [1, 3, 6, 7, 11]
    K = 18
    N = len(arr)
    findPoint(arr, N, K)

    # This code is contributed by SURENDRA_GANGWAR.**
```

## ****C#****

```
**// C# program for the above approach
using System;

class GFG{

// Function to find the sum of distances
// of all points from a given point
public static int findSum(int[] arr, int N, int pt)
{

    // Stores sum of distances
    int sum = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {
        sum += Math.Abs(arr[i] - pt);
    }

    // Return the sum
    return sum;
}

// Function to find such a point having
// sum of distances of all other points
// from this point equal to K
public static void findPoint(int[] arr, int N, int K)
{

    // If N is odd keep left as arr[n / 2]
    // else keep left as arr[n / 2 - 1] + 1;
    int left;

    if (N % 2 != 0)
    {
        left = arr[N / 2];
    }
    else
    {
        left = arr[N / 2 - 1] + 1;
    }

    // Keep right as arr[N - 1]
    int right = arr[N - 1];

    // Perform binary search in the
    // right half
    while (left <= right)
    {

        // Calculate the mid index
        // of the range
        int mid = (left + right) / 2;

        int temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K)
        {

            // Print the value of mid
            Console.WriteLine(mid);
            return;
        }

        // If the value of K < temp
        else if (K < temp)
        {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If the value of K > temp
        else
        {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // Update the value of left
    left = arr[0];

    // Update the value of right
    right = arr[N / 2] - 1;

    // Perform binary search on the
    // left half
    while (left <= right)
    {

        // Calculate the mid index
        // of the range
        int mid = (left + right) / 2;

        int temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K)
        {

            // Print mid
            Console.WriteLine(mid);
            return;
        }

        // if K > temp
        else if (K > temp)
        {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If K < temp
        else
        {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // If no such point found
    Console.WriteLine("-1");
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 1, 3, 6, 7, 11 };
    int K = 18;
    int N = arr.Length;

    findPoint(arr, N, K);
}
}

// This code is contributed by ukasp**
```

## ****java 描述语言****

```
**<script>

// Jaascript program for the above approach

// Function to find the sum of distances
// of all points from a given point
function findSum(arr, N, pt)
{

    // Stores sum of distances
    var sum = 0;
    var i;

    // Traverse the array
    for(i = 0; i < N; i++)
    {
        sum += Math.abs(arr[i] - pt);
    }

    // Return the sum
    return sum;
}

// Function to find such a point having
// sum of distances of all other points
// from this point equal to K
function findPoint(arr, N, K)
{

    // If N is odd keep left as arr[n / 2]
    // else keep left as arr[n / 2 - 1] + 1;
    var left;

    if (N % 2 == 1)
    {
        left = arr[parseInt(N / 2)];
    }
    else
    {
        left = arr[parseInt(N / 2) - 1] + 1;
    }

    // Keep right as arr[N - 1]
    var right = arr[N - 1];

    // Perform binary search in the
    // right half
    while (left <= right)
    {

        // Calculate the mid index
        // of the range
        var mid = parseInt((left + right) / 2);

        var temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K)
        {

            // Print the value of mid
            document.write(mid);
            return;
        }

        // If the value of K < temp
        else if (K < temp)
        {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If the value of K > temp
        else
        {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // Update the value of left
    left = arr[0];

    // Update the value of right
    right = arr[parseInt(N / 2)] - 1;

    // Perform binary search on the
    // left half
    while (left <= right)
    {

        // Calculate the mid index
        // of the range
        var mid = parseInt((left + right) / 2);

        var temp = findSum(arr, N, mid);

        // If temp is equal to K
        if (temp == K)
        {

            // Print mid
            document.write(mid);
            return;
        }

        // If K > temp
        else if (K > temp)
        {

            // Update right to mid - 1
            right = mid - 1;
        }

        // If K < temp
        else
        {

            // Update left to mid + 1
            left = mid + 1;
        }
    }

    // If no such point found
    document.write("-1");
}

// Driver Code
var arr = [ 1, 3, 6, 7, 11 ];
var K = 18;
var N = arr.length;

findPoint(arr, N, K);

// This code is contributed by bgangwar59

</script>**
```

******Output:** 

```
8
```**** 

*******时间复杂度:**O(N * log<sub>2</sub>(M–M))其中 **M** 为数组的最大值， **m** 为数组的* [*最小值。*](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)
***辅助空间:** O(1)*****