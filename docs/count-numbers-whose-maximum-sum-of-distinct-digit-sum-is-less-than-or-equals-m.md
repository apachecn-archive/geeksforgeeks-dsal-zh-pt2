# 计算不同数字和的最大和小于或等于 M 的数字

> 原文:[https://www . geesforgeks . org/count-numbers-其最大非重复数字总和小于或等于-m/](https://www.geeksforgeeks.org/count-numbers-whose-maximum-sum-of-distinct-digit-sum-is-less-than-or-equals-m/)

给定一个整数数组 **arr[]** 和一个数字 **M** ，任务是找出不同数字和之和小于或等于给定数字 **M** 的数字的最大计数。

**示例:**

> **输入:** arr[] = {1，45，16，17，219，32，22}，M = 10
> **输出:** 3
> **解释:**
> 数组的数字和为–{ 1，9，7，8，12，5，4}
> 小于 M 的不同数字和的最大和为{1 + 5 + 4}
> 因此，此类数字的计数为 3。
> 
> **输入:** arr[] = {32，45}，M = 2
> **输出:** 0
> **解释:**
> 数组的数字和为–{ 5，9}
> 小于 M 的不同数字和的最大和为 0
> 因此，此类数字的计数为 0。

**方法:**
思路是找到数组中每个元素的[数字和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)，然后[排序](https://www.geeksforgeeks.org/merge-sort/)数字和数组。
现在问题归结为从排序的不同数字和数组中计数元素的数量，总和小于或等于 M。
为此，取最小的不同数字和，直到这些数字的总和小于或等于给定的数量 **M** 并返回这些数字的计数。

**举例说明:**

```
Given Array be - arr[] = {1, 45, 17, 32, 22}, M = 10

Then Digit-sum of each number in the array - 
Digit-sum(1) = 1
Digit-sum(45) = 4 + 5 = 9
Digit-sum(17) = 1 + 7 = 8
Digit-sum(32) = 3 + 2 = 5
Digit-sum(22) = 2 + 2 = 4

After sorting the digit-sum array - 
Digit-sum[] = {1, 4, 5, 8, 9}

Then there are three numbers such that, 
there sum is less than or equal to M = 10
which is {1, 4, 5} 
Sum = 1 + 4 + 5 = 10 &leq; M
```

**算法:**

*   找到数组中每个元素的[数字和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)，并将其存储在另一个数组中(比如**数字和[]** )
*   [按递增顺序排列**数字和[]** 数组。](https://www.geeksforgeeks.org/merge-sort/)
*   从排序的数字和[]数组中删除重复的元素，以便只有唯一的数字和。
*   将变量**和**初始化为 0，以存储当前和。
*   迭代数字和[]数组，并将元素添加到**和**中，直到**和**的值小于或等于 **M** 并增加计数。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// Maximum count of numbers whose
// sum of distinct digit-sum less
// than or equal to the given number

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// digit-sum of a number
int SumofDigits(int digit)
{
    int sum = 0;

    // Loop to iterate the number
    // digit-wise to find digit-sum
    while (digit != 0) {

        // variable to store last digit
        int rem = digit % 10;
        sum += rem;
        digit /= 10;
    }
    return sum;
}

// Function to find the count of number
int findCountofNumbers(int arr[],
                   int n, int M){

    // Vector to store the Sum of Digits
    vector<int> SumDigits;

    // Sum of digits for each
    // element in vector
    for (int i = 0; i < n; i++) {
        int s = SumofDigits(arr[i]);
        SumDigits.push_back(s);
    }

    // Sorting the digitSum vector
    sort(SumDigits.begin(), SumDigits.end());

    // Removing the duplicate elements
    vector<int>::iterator ip;
    ip = unique(SumDigits.begin(),
                 SumDigits.end());
    SumDigits.resize(distance(
         SumDigits.begin(), ip)
         );

    // Count variable to store the Count
    int count = 0;
    int sum = 0;
    // Finding the Count of Numbers
    for (int i = 0; i < SumDigits.size(); i++) {
        if (sum > M)
            break;
        sum += SumDigits[i];
        if (sum <= M)
            count++;
    }
    return count;
}

// Driver Code
int main()
{

    int arr[] = { 1, 45, 16, 17,
           219, 32, 22 }, M = 10;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findCountofNumbers(arr, n, M);
    return 0;
}
```

## 蟒蛇 3

```
# Python 3 implementation to find the
# Maximum count of numbers whose
# sum of distinct digit-sum less
# than or equal to the given number

# Function to find the
# digit-sum of a number
def SumofDigits( digit):

    sum = 0

    # Loop to iterate the number
    # digit-wise to find digit-sum
    while (digit != 0):

        # variable to store last digit
        rem = digit % 10
        sum += rem
        digit //= 10

    return sum

# Function to find the count of number
def findCountofNumbers(arr, n, M):

    # Vector to store the Sum of Digits
    SumDigits = []

    # Sum of digits for each
    # element in vector
    for i in range( n ):
        s = SumofDigits(arr[i])
        SumDigits.append(s)

    # Sorting the digitSum vector
    SumDigits.sort()

    # Removing the duplicate elements
    ip = list(set(SumDigits))

    # Count variable to store the Count
    count = 0
    sum = 0

    # Finding the Count of Numbers
    for i in range(len(SumDigits)):
        if (sum > M):
            break
        sum += SumDigits[i]
        if (sum <= M):
            count+=1

    return count

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 45, 16, 17,
        219, 32, 22 ]
    M = 10
    n = len(arr)

    # Function Call
    print( findCountofNumbers(arr, n, M))

# This ccode is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// Maximum count of numbers whose
// sum of distinct digit-sum less
// than or equal to the given number

// Function to find the
// digit-sum of a number
function SumofDigits(digit)
{
    let sum = 0;

    // Loop to iterate the number
    // digit-wise to find digit-sum
    while (digit != 0)
    {

        // Variable to store last digit
        let rem = digit % 10;
        sum += rem;
        digit = Math.floor(digit/10);
    }
    return sum;
}

// Function to find the count of number
function findCountofNumbers(arr, n, M)
{

    // Vector to store the Sum of Digits
    let SumDigits = [];

    // Sum of digits for each
    // element in vector
    for(let i = 0; i < n; i++)
    {
        let s = SumofDigits(arr[i]);
        SumDigits.push(s);
    }

    // Sorting the digitSum vector
    SumDigits.sort(function(a, b){return a - b;});

    // Removing the duplicate elements
    let ip = Array.from(new Set(SumDigits));

    // Count variable to store the Count
    let count = 0;
    let sum = 0;

    // Finding the Count of Numbers
    for(let i = 0; i < SumDigits.length; i++)
    {
        if (sum > M)
            break;

        sum += SumDigits[i];

        if (sum <= M)
            count++;
    }
    return count;
}

// Driver Code
let arr = [ 1, 45, 16, 17,
            219, 32, 22 ];
let M = 10;
let n = arr.length;

// Function Call
document.write(findCountofNumbers(arr, n, M));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
3
```

**性能分析:**

*   **时间复杂度:**在给定的方法中，我们使用排序，在最坏的情况下取 O(NlogN)并且求每个元素的数字和取 O(N*K)，其中 K 是最大位数，因此时间复杂度将是 **O(NlogN + N*k)** 。
*   **辅助空间:** O(N)