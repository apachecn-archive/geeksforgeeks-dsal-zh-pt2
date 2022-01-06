# 一个和为完美立方体的数组中对的计数

> 原文:[https://www . geeksforgeeks . org/数组中的对数-其和为完美立方/](https://www.geeksforgeeks.org/count-of-pairs-in-an-array-whose-sum-is-a-perfect-cube/)

给定一个由大小不同的元素组成的数组****N**，任务是找出数组中的总对数，其和为一个[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。
**举例:**** 

> ****输入:** arr[] = {2，3，6，9，10，20}
> **输出:** 1
> 唯一可能的对是(2，6)
> **输入:** arr[] = {9，2，5，1}
> **输出:** 0**

****天真方法:**使用[嵌套循环](https://www.geeksforgeeks.org/java-nested-loops-with-examples/)并检查每一个可能的对，看它们的和是否是[完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。当数组的长度很大时，这种技术是无效的。
**高效方法:**** 

*   **将数组的所有元素存储在一个 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 中，并将最大两个元素的总和保存在一个名为 **max** 的变量中。**
*   **很明显，数组中任意两个元素的和都不会超过 **max** 。所以，找到所有完美立方体**最大**并保存在名为**完美立方体**的数组列表中。**
*   **现在对数组中的每个元素说 **arr[i]** ，对保存在 **perfectcubes** 中的每个完美立方体，检查**perfect cubes . get(I)–arr[I]**是否存在于 **nums** 中，即如果原始数组中有任何元素，当与当前选择的元素相加时，给出列表中的任何完美立方体。**
*   **如果满足上述条件，增加**计数**变量。**
*   **最后打印**计数**的值。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include<bits/stdc++.h>
#include<vector>
using namespace std;

// Function to return an ArrayList containing
// all the perfect cubes upto n
vector<int> getPerfectcubes(int n)
{

    vector<int>perfectcubes;
    int current = 1;
    int i = 1;

    // while current perfect cube is
    // less than or equal to n
    while (current <= n)
    {
        perfectcubes.push_back(current);
        i += 1;
        current = int(pow(i, 3));
    }
    return perfectcubes;
}

// Function to print the sum of maximum
// two elements from the array
int maxPairSum(int arr[],int n)
{

    int max = 0;
    int secondMax = 0;
    if (arr[0] > arr[1])
    {
        max = arr[0];
        secondMax = arr[1];
    }
    else
    {
        max = arr[1];
        secondMax = arr[0];
    }
    for (int i = 2; i < n; i++)
    {
        if (arr[i] > max)
        {
            secondMax = max;
            max = arr[i];
        }
        else if (arr[i] > secondMax)
            secondMax = arr[i];
    }
    return (max + secondMax);
}

// Function to return the count of numbers that
// when added with n give a perfect cube
int countPairsWith(int n, vector<int> perfectcubes, vector<int> nums)
{

    int count = 0;
    int len=perfectcubes.size();
    for (int i = 0; i < len; i++)
    {
        int temp = perfectcubes[i] - n;

        // temp > n is checked so that pairs
        // (x, y) and (y, x) don't get counted twice
        if (temp > n)
        {
            for(auto j=nums.begin();j!=nums.end();j++)
            {
                if((*j)==temp)
                    count += 1;
            }
        }
    }
    return count;
}

// Function to count the pairs whose
// sum is a perfect cube
int countPairs(int arr[],int n)
{

    // Sum of the maximum two elements
    // from the array
    int max = maxPairSum(arr,n);

    // List of perfect cubes upto max
    vector<int>perfectcubes = getPerfectcubes(max);

    // Contains all the array elements
    vector<int>nums;
    for (int i = 0 ; i < n; i++)
        nums.push_back(arr[i]);

    int count = 0;
    for (int i = 0; i < n; i++)
    {

        // Add count of the elements that when
        // added with arr[i] give a perfect cube
        count += countPairsWith(arr[i], perfectcubes, nums);
    }
    return count;

}

// Driver code
int main()
{
    int arr[] = { 2, 6, 18, 9, 999, 1 };
    int n=sizeof(arr)/sizeof(arr[0]);
    cout<<(countPairs(arr,n));

}

// This code is contributed by chitranayal
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return an ArrayList containing
    // all the perfect cubes upto n
    static List<Integer> getPerfectcubes(int n) {

        List<Integer> perfectcubes = new ArrayList<Integer>();
        int current = 1;
        int i = 1;

        // while current perfect cube is
        // less than or equal to n
        while (current <= n) {
            perfectcubes.add(current);
            i += 1;
            current = (int) (Math.pow(i, 3));
        }
        return perfectcubes;
    }

    // Function to print the sum of maximum
    // two elements from the array
    static int maxPairSum(int[] arr) {

        int n = arr.length;
        int max = 0;
        int secondMax = 0;
        if (arr[0] > arr[1]) {
            max = arr[0];
            secondMax = arr[1];
        } else {
            max = arr[1];
            secondMax = arr[0];
        }
        for (int i = 2; i < n; i++) {
            if (arr[i] > max) {
                secondMax = max;
                max = arr[i];
            } else if (arr[i] > secondMax) {
                secondMax = arr[i];
            }
        }
        return (max + secondMax);
    }

    // Function to return the count of numbers that
    // when added with n give a perfect cube
    static int countPairsWith(int n, List<Integer>
            perfectcubes, List<Integer> nums) {

        int count = 0;
        for (int i = 0; i < perfectcubes.size(); i++) {
            int temp = perfectcubes.get(i) - n;

            // temp > n is checked so that pairs
            // (x, y) and (y, x) don't get counted twice
            if (temp > n && (nums.contains(temp)))
                count += 1;
        }
        return count;
    }

    // Function to count the pairs whose
    // sum is a perfect cube
    static int countPairs(int[] arr) {

        int n = arr.length;

        // Sum of the maximum two elements
        // from the array
        int max = maxPairSum(arr);

        // List of perfect cubes upto max
        List<Integer> perfectcubes = getPerfectcubes(max);

        // Contains all the array elements
        List<Integer> nums = new ArrayList<Integer>();
        for (int i = 0; i < n; i++) {
            nums.add(arr[i]);
        }
        int count = 0;
        for (int i = 0; i < n; i++) {

            // Add count of the elements that when
            // added with arr[i] give a perfect cube
            count += countPairsWith(arr[i], perfectcubes, nums);
        }
        return count;
    }

    // Driver code
    public static void main(String[] agrs) {
        int[] arr = { 2, 6, 18, 9, 999, 1 };
        System.out.print(countPairs(arr));
    }
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 implementation of the approach

# Function to return an ArrayList containing
# all the perfect cubes upto n
def getPerfectcubes(n):

    perfectcubes = [];
    current = 1;
    i = 1;

    # while current perfect cube is
    # less than or equal to n
    while (current <= n):
        perfectcubes.append(current);
        i += 1;
        current = int(pow(i, 3));

    return perfectcubes;

# Function to print the sum of maximum
# two elements from the array
def maxPairSum(arr):

    n = len(arr);
    max = 0;
    secondMax = 0;
    if (arr[0] > arr[1]):
        max = arr[0];
        secondMax = arr[1];
    else:
        max = arr[1];
        secondMax = arr[0];

    for i in range(2, n):
        if (arr[i] > max):
            secondMax = max;
            max = arr[i];
        elif (arr[i] > secondMax):
            secondMax = arr[i];

    return (max + secondMax);

# Function to return the count of numbers that
# when added with n give a perfect cube
def countPairsWith(n, perfectcubes, nums):

    count = 0;
    for i in range(len(perfectcubes)):
        temp = perfectcubes[i] - n;

        # temp > n is checked so that pairs
        # (x, y) and (y, x) don't get counted twice
        if (temp > n and (temp in nums)):
            count += 1;

    return count;

# Function to count the pairs whose
# sum is a perfect cube
def countPairs(arr):

    n = len(arr);

    # Sum of the maximum two elements
    # from the array
    max = maxPairSum(arr);

    # List of perfect cubes upto max
    perfectcubes = getPerfectcubes(max);

    # Contains all the array elements
    nums = [];
    for i in range(n):
        nums.append(arr[i]);

    count = 0;
    for i in range(n):

        # Add count of the elements that when
        # added with arr[i] give a perfect cube
        count += countPairsWith(arr[i],
                perfectcubes, nums);
    return count;

# Driver code
arr = [ 2, 6, 18, 9, 999, 1 ];
print(countPairs(arr));
```

## **C#**

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return an List containing
    // all the perfect cubes upto n
    static List<int> getPerfectcubes(int n) {

        List<int> perfectcubes = new List<int>();
        int current = 1;
        int i = 1;

        // while current perfect cube is
        // less than or equal to n
        while (current <= n) {
            perfectcubes.Add(current);
            i += 1;
            current = (int) (Math.Pow(i, 3));
        }
        return perfectcubes;
    }

    // Function to print the sum of maximum
    // two elements from the array
    static int maxPairSum(int[] arr) {

        int n = arr.Length;
        int max = 0;
        int secondMax = 0;
        if (arr[0] > arr[1]) {
            max = arr[0];
            secondMax = arr[1];
        } else {
            max = arr[1];
            secondMax = arr[0];
        }
        for (int i = 2; i < n; i++) {
            if (arr[i] > max) {
                secondMax = max;
                max = arr[i];
            } else if (arr[i] > secondMax) {
                secondMax = arr[i];
            }
        }
        return (max + secondMax);
    }

    // Function to return the count of numbers that
    // when added with n give a perfect cube
    static int countPairsWith(int n, List<int>
            perfectcubes, List<int> nums) {

        int count = 0;
        for (int i = 0; i < perfectcubes.Count; i++) {
            int temp = perfectcubes[i] - n;

            // temp > n is checked so that pairs
            // (x, y) and (y, x) don't get counted twice
            if (temp > n && (nums.Contains(temp)))
                count += 1;
        }
        return count;
    }

    // Function to count the pairs whose
    // sum is a perfect cube
    static int countPairs(int[] arr) {

        int n = arr.Length;

        // Sum of the maximum two elements
        // from the array
        int max = maxPairSum(arr);

        // List of perfect cubes upto max
        List<int> perfectcubes = getPerfectcubes(max);

        // Contains all the array elements
        List<int> nums = new List<int>();
        for (int i = 0; i < n; i++) {
            nums.Add(arr[i]);
        }
        int count = 0;
        for (int i = 0; i < n; i++) {

            // Add count of the elements that when
            // added with arr[i] give a perfect cube
            count += countPairsWith(arr[i], perfectcubes, nums);
        }
        return count;
    }

    // Driver code
    public static void Main(String[] agrs) {
        int[] arr = { 2, 6, 18, 9, 999, 1 };
        Console.Write(countPairs(arr));
    }
}

// This code contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

// Function to return an ArrayList containing
// all the perfect cubes upto n
function getPerfectcubes(n)
{

    let perfectcubes = [];
    let current = 1;
    let i = 1;

    // while current perfect cube is
    // less than or equal to n
    while (current <= n)
    {
        perfectcubes.push(current);
        i += 1;
        current = parseInt(Math.pow(i, 3));
    }
    return perfectcubes;
}

// Function to print the sum of maximum
// two elements from the array
function maxPairSum(arr,n)
{

    let max = 0;
    let secondMax = 0;
    if (arr[0] > arr[1])
    {
        max = arr[0];
        secondMax = arr[1];
    }
    else
    {
        max = arr[1];
        secondMax = arr[0];
    }
    for (let i = 2; i < n; i++)
    {
        if (arr[i] > max)
        {
            secondMax = max;
            max = arr[i];
        }
        else if (arr[i] > secondMax)
            secondMax = arr[i];
    }
    return (max + secondMax);
}

// Function to return the count of numbers that
// when added with n give a perfect cube
function countPairsWith(n, perfectcubes, nums)
{

    let count = 0;
    let len=perfectcubes.length;
    for (let i = 0; i < len; i++)
    {
        let temp = perfectcubes[i] - n;

        // temp > n is checked so that pairs
        // (x, y) and (y, x) don't get counted twice
        if (temp > n)
        {
            for(let j = 0; j < nums.length; j++)
            {
                if(nums[j] == temp)
                    count += 1;
            }
        }
    }
    return count;
}

// Function to count the pairs whose
// sum is a perfect cube
function countPairs(arr,n)
{

    // Sum of the maximum two elements
    // from the array
    let max = maxPairSum(arr,n);

    // List of perfect cubes upto max
    let perfectcubes = getPerfectcubes(max);

    // Contains all the array elements
    let nums = [];
    for (let i = 0 ; i < n; i++)
        nums.push(arr[i]);

    let count = 0;
    for (let i = 0; i < n; i++)
    {

        // Add count of the elements that when
        // added with arr[i] give a perfect cube
        count += countPairsWith(arr[i], perfectcubes, nums);
    }
    return count;

}

// Driver code
let arr = [ 2, 6, 18, 9, 999, 1 ];
let n = arr.length;
document.write(countPairs(arr,n));

</script>
```

****Output:** 

```
3
```** 

**时间复杂度:O(n <sup>3</sup> )**

**辅助空间:O(n)**