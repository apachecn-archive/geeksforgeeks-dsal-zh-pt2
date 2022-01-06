# 在数组中找到一个三元组，其和最接近给定的数

> 原文:[https://www . geeksforgeeks . org/find-a-three-in-in-a-array-其和最接近给定的数字/](https://www.geeksforgeeks.org/find-a-triplet-in-an-array-whose-sum-is-closest-to-a-given-number/)

给定一个由 **N** 个整数和一个整数 **X** 组成的数组 **arr[]** ，任务是在 **arr[]** 中找到三个整数，使得和最接近 **X** 。

**示例:**

```
Input: arr[] = {-1, 2, 1, -4}, X = 1
Output: 2
Explanation:
Sums of triplets:
(-1) + 2 + 1 = 2
(-1) + 2 + (-4) = -3
2 + 1 + (-4) = -1
2 is closest to 1.

Input: arr[] = {1, 2, 3, 4, -5}, X = 10
Output: 9
Explanation:
Sums of triplets:
1 + 2 + 3 = 6
2 + 3 + 4 = 9
1 + 3 + 4 = 7
...
9 is closest to 10.
```

**<u>简单方法:</u>** 天真的方法是探索大小为 3 的所有子集，并跟踪 X 和这个子集的和之间的差异。然后返回其和与 X 之差最小的子集。

**算法:**

1.  分别用计数器 I、j 和 k 创建三个嵌套循环。
2.  第一个循环从开始到结束，第二个循环从 i+1 到结束，第三个循环从 j+1 到结束。
3.  检查 ith、jth 和 kth 元素的和与给定和的差是否小于当前最小值。更新当前最小值
4.  打印最接近的总和。

**实施:**

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of a
// triplet which is closest to x
int solution(vector<int>& arr, int x)
{
    // To store the closest sum
    int closestSum = INT_MAX;

    // Run three nested loops each loop
    // for each element of triplet
    for (int i = 0; i < arr.size() ; i++)
    {
        for(int j =i + 1; j < arr.size(); j++)
        {
            for(int k =j + 1; k < arr.size(); k++)
            {
                //update the closestSum
                if(abs(x - closestSum) > abs(x - (arr[i] + arr[j] + arr[k])))
                    closestSum = (arr[i] + arr[j] + arr[k]);
            }
        }
    }
    // Return the closest sum found
    return closestSum;
}

// Driver code
int main()
{
    vector<int> arr = { -1, 2, 1, -4 };
    int x = 1;
    cout << solution(arr, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to return the sum of a
// triplet which is closest to x
public static int solution(int arr[], int x)
{

    // To store the closest sum
    int closestSum = Integer.MAX_VALUE;

    // Run three nested loops each loop 
    // for each element of triplet
    for(int i = 0; i < arr.length ; i++) 
    {
        for(int j = i + 1; j < arr.length; j++)
        {
            for(int k = j + 1; k < arr.length; k++)
            {

                // Update the closestSum
                if (Math.abs(x - closestSum) >
                    Math.abs(x - (arr[i] + arr[j] + arr[k])))
                    closestSum = (arr[i] + arr[j] + arr[k]);
            } 
        }
    }

    // Return the closest sum found
    return closestSum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { -1, 2, 1, -4 };
    int x = 1;

    System.out.print(solution(arr, x));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
import sys

# Function to return the sum of a
# triplet which is closest to x
def solution(arr, x):

    # To store the closest sum
    closestSum = sys.maxsize

    # Run three nested loops each loop
    # for each element of triplet
    for i in range (len(arr)) :
        for j in range(i + 1, len(arr)):
            for k in range(j + 1, len( arr)):

                # Update the closestSum
                if(abs(x - closestSum) >
                abs(x - (arr[i] +
                arr[j] + arr[k]))):
                    closestSum = (arr[i] +
                                    arr[j] + arr[k])

    # Return the closest sum found
    return closestSum

# Driver code
if __name__ == "__main__":

    arr = [ -1, 2, 1, -4 ]
    x = 1

    print(solution(arr, x))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to return the sum of a
// triplet which is closest to x
static int solution(ArrayList arr, int x)
{

    // To store the closest sum
    int closestSum = int.MaxValue;

    // Run three nested loops each loop
    // for each element of triplet
    for(int i = 0; i < arr.Count; i++)
    {
        for(int j = i + 1; j < arr.Count; j++)
        {
            for(int k = j + 1; k < arr.Count; k++)
            {
                if (Math.Abs(x - closestSum) >
                    Math.Abs(x - ((int)arr[i] +
                   (int)arr[j] + (int)arr[k])))
                {
                    closestSum = ((int)arr[i] +
                                  (int)arr[j] +
                                  (int)arr[k]);
                }
            }
        }
    }

    // Return the closest sum found
    return closestSum;
}

// Driver code
public static void Main(string[] args)
{
    ArrayList arr = new ArrayList(){ -1, 2, 1, -4 };
    int x = 1;
    Console.Write(solution(arr, x));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the sum of a
// triplet which is closest to x
function solution(arr, x)
{

    // To store the closest sum
    let closestSum = Number.MAX_VALUE;

    // Run three nested loops each loop
    // for each element of triplet
    for(let i = 0; i < arr.length ; i++)
    {
        for(let j =i + 1; j < arr.length; j++)
        {
            for(let k =j + 1; k < arr.length; k++)
            {

                // Update the closestSum
                if (Math.abs(x - closestSum) >
                    Math.abs(x - (arr[i] + arr[j] + arr[k])))
                    closestSum = (arr[i] + arr[j] + arr[k]);
            }
        }
    }

    // Return the closest sum found
    return closestSum;
}

// Driver code
let arr = [ -1, 2, 1, -4 ];
let x = 1;

document.write(solution(arr, x));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
2
```

**复杂度分析:**

*   **时间复杂度:** O(N <sup>3</sup> )。
    三个嵌套循环在数组中遍历，因此时间复杂度为 O(n^3).
*   **空间**复杂度 **:** O(1)。
    因为不需要额外的空间。

**<u>高效方法:</u>** 通过对数组进行排序可以提高算法的效率。这种高效的方法使用了[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)。遍历数组并固定三元组的第一个元素。现在使用双指针算法找到最接近*x–数组【I】*的数字。更新最接近的总和。两点算法需要线性时间，因此比嵌套循环更好。

**算法:**

1.  给定数组排序。
2.  循环数组并固定可能三元组的第一个元素，arr[i]。
3.  然后固定**两个指针**，一个在 I **+ 1** ，另一个在**n–1**。看看总数，
    *   如果和小于我们需要得到的和，我们增加第一个指针。
    *   否则，如果总和较大，减少结束指针以减少总和。
    *   更新到目前为止找到的最接近的总和。

**实施:**

## C++14

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the sum of a
// triplet which is closest to x
int solution(vector<int>& arr, int x)
{

    // Sort the array
    sort(arr.begin(), arr.end());

    // To store the closest sum
  //not using INT_MAX to avoid overflowing condition
    int closestSum = 1000000000;

    // Fix the smallest number among
    // the three integers
    for (int i = 0; i < arr.size() - 2; i++) {

        // Two pointers initially pointing at
        // the last and the element
        // next to the fixed element
        int ptr1 = i + 1, ptr2 = arr.size() - 1;

        // While there could be more pairs to check
        while (ptr1 < ptr2) {

            // Calculate the sum of the current triplet
            int sum = arr[i] + arr[ptr1] + arr[ptr2];

              // if sum is equal to x, return sum as
              if (sum == x)
              return sum;
            // If the sum is more closer than
            // the current closest sum
            if (abs(x - sum) < abs(x - closestSum)) {
                closestSum = sum;
            }

            // If sum is greater then x then decrement
            // the second pointer to get a smaller sum
            if (sum > x) {
                ptr2--;
            }

            // Else increment the first pointer
            // to get a larger sum
            else {
                ptr1++;
            }
        }
    }

    // Return the closest sum found
    return closestSum;
}

// Driver code
int main()
{
    vector<int> arr = { -1, 2, 1, -4 };
    int x = 1;
    cout << solution(arr, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import static java.lang.Math.abs;
import java.util.*;

class GFG
{

// Function to return the sum of a
// triplet which is closest to x
static int solution(Vector<Integer> arr, int x)
{

    // Sort the array
    Collections.sort(arr);

    // To store the closest sum
      // Assigning long to avoid overflow condition
      // when array has negative integers
    long closestSum = Integer.MAX_VALUE;

    // Fix the smallest number among
    // the three integers
    for (int i = 0; i < arr.size() - 2; i++)
    {

        // Two pointers initially pointing at
        // the last and the element
        // next to the fixed element
        int ptr1 = i + 1, ptr2 = arr.size() - 1;

        // While there could be more pairs to check
        while (ptr1 < ptr2)
        {

            // Calculate the sum of the current triplet
            int sum = arr.get(i) + arr.get(ptr1) + arr.get(ptr2);

            // If the sum is more closer than
            // the current closest sum
            if (abs(x - sum) < abs(x - closestSum))
            {
                closestSum = sum;
            }

            // If sum is greater then x then decrement
            // the second pointer to get a smaller sum
            if (sum > x)
            {
                ptr2--;
            }

            // Else increment the first pointer
            // to get a larger sum
            else
            {
                ptr1++;
            }
        }
    }

    // Return the closest sum found
    return (int)closestSum;
}

// Driver code
public static void main(String[] args)
{
    Vector arr = new Vector(Arrays.asList( -1, 2, 1, -4 ));
    int x = 1;
    System.out.println(solution(arr, x));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

import sys

# Function to return the sum of a
# triplet which is closest to x
def solution(arr, x) :

    # Sort the array
    arr.sort();

    # To store the closest sum
    closestSum = sys.maxsize;

    # Fix the smallest number among
    # the three integers
    for i in range(len(arr)-2) :

        # Two pointers initially pointing at
        # the last and the element
        # next to the fixed element
        ptr1 = i + 1; ptr2 = len(arr) - 1;

        # While there could be more pairs to check
        while (ptr1 < ptr2) :

            # Calculate the sum of the current triplet
            sum = arr[i] + arr[ptr1] + arr[ptr2];

            # If the sum is more closer than
            # the current closest sum
            if (abs(x - sum) < abs(x - closestSum)) :
                closestSum = sum;

            # If sum is greater then x then decrement
            # the second pointer to get a smaller sum
            if (sum > x) :
                ptr2 -= 1;

            # Else increment the first pointer
            # to get a larger sum
            else :
                ptr1 += 1;

    # Return the closest sum found
    return closestSum;

# Driver code
if __name__ == "__main__" :

    arr = [ -1, 2, 1, -4 ];
    x = 1;
    print(solution(arr, x));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the sum of a
// triplet which is closest to x
static int solution(List<int> arr, int x)
{

    // Sort the array
    arr.Sort();

    // To store the closest sum
    int closestSum = int.MaxValue;

    // Fix the smallest number among
    // the three integers
    for (int i = 0; i < arr.Count - 2; i++)
    {

        // Two pointers initially pointing at
        // the last and the element
        // next to the fixed element
        int ptr1 = i + 1, ptr2 = arr.Count - 1;

        // While there could be more pairs to check
        while (ptr1 < ptr2)
        {

            // Calculate the sum of the current triplet
            int sum = arr[i] + arr[ptr1] + arr[ptr2];

            // If the sum is more closer than
            // the current closest sum
            if (Math.Abs(x - sum) <
                Math.Abs(x - closestSum))
            {
                closestSum = sum;
            }

            // If sum is greater then x then decrement
            // the second pointer to get a smaller sum
            if (sum > x)
            {
                ptr2--;
            }

            // Else increment the first pointer
            // to get a larger sum
            else
            {
                ptr1++;
            }
        }
    }

    // Return the closest sum found
    return closestSum;
}

// Driver code
public static void Main(String[] args)
{
    int []ar = { -1, 2, 1, -4 };
    List<int> arr = new List<int>(ar);
    int x = 1;
    Console.WriteLine(solution(arr, x));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the sum of a
// triplet which is closest to x
function solution(arr, x)
{

    // Sort the array
    arr.sort((a, b) => a - b);

    // To store the closest sum
   // not using INT_MAX to avoid
   // overflowing condition
    let closestSum = 1000000000;

    // Fix the smallest number among
    // the three integers
    for (let i = 0; i < arr.length - 2; i++)
    {

        // Two pointers initially pointing at
        // the last and the element
        // next to the fixed element
        let ptr1 = i + 1, ptr2 = arr.length - 1;

        // While there could be more pairs to check
        while (ptr1 < ptr2) {

            // Calculate the sum of the current triplet
            let sum = arr[i] + arr[ptr1] + arr[ptr2];

            // If the sum is more closer than
            // the current closest sum
            if (Math.abs(1*x - sum) < Math.abs(1*x - closestSum))
            {
                closestSum = sum;
            }

            // If sum is greater then x then decrement
            // the second pointer to get a smaller sum
            if (sum > x) {
                ptr2--;
            }

            // Else increment the first pointer
            // to get a larger sum
            else {
                ptr1++;
            }
        }
    }

    // Return the closest sum found
    return closestSum;
}

// Driver code
    let arr = [ -1, 2, 1, -4 ];
    let x = 1;
    document.write(solution(arr, x));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
2
```

**复杂度分析:**

*   **时间复杂度:O(N <sup>2</sup> )** 。
    只有两个嵌套循环遍历数组，因此时间复杂度是 O(n^2).双指针算法花费 O(n)个时间，第一个元素可以使用另一个嵌套遍历来固定。
*   **空间**复杂度 **: O(1)** 。
    因为不需要额外的空间。