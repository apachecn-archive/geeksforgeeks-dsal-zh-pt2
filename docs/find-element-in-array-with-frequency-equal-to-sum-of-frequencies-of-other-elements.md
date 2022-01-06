# 查找数组中频率等于其他元素频率之和的元素

> 原文:[https://www . geesforgeks . org/find-频率等于其他元素频率之和的数组元素/](https://www.geeksforgeeks.org/find-element-in-array-with-frequency-equal-to-sum-of-frequencies-of-other-elements/)

给定一个整数数组 **arr[]** ，任务是在数组中找到一个元素，其频率等于数组中其他元素的频率之和。

**示例:**

> **输入:** arr[] = {1，2，2，3，3，3}
> **输出:** 3
> **解释:**
> 数组元素的频率–
> 频率(3) = 3
> 频率(2) = 2
> 频率(1) = 1
> 这里，元素 3 的频率等于
> 数组其他元素的频率之和。
> 
> **输入:** arr[] = {1，2，3}
> **输出:** -1
> **说明:**
> 在上面给定的数组中，不存在这样的
> 元素，其频率等于数组中其他元素的
> 频率之和。

**方法:**问题中的关键观察是，如果数组的长度是奇数，那么就不会有这样的元素，而在偶数长度数组的情况下，计算数组每个元素的[频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)，然后最后，检查数组中频率等于数组半长的任何元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// element whose frequency is equal
// to the sum of frequencies of
// other elements of the array

#include <bits/stdc++.h>
using namespace std;

// Function to check that any element
// have frequency equal to the sum of
// frequency of other elements of the array
bool isFrequencyEqual(int arr[], int len)
{
    // Check that if the array length
    // is odd, Then no solution possible
    if (len % 2 == 1){
        cout << "No Such Element";
        return false;
    }

    // Hash-map to store the frequency
    // of elements of array
    map<int, int> freq;

    // Loop to find the frequency
    // of elements of array
    for (int i = 0; i < len; i++)
        freq[arr[i]]++;

    // Loop to check if any element
    // of the array have frequency
    // equal to the half length
    for (int i = 0; i < len; i++){
        if (freq[arr[i]] == len / 2){
            cout << arr[i] << endl;
            return true;
        }
    }

    cout << "No such element";
    return false;
}

// Driver Code
int main()
{
    int arr[6] = { 1, 2, 2, 3, 3, 3 };
    int n = 6;

    // Function Call
    isFrequencyEqual(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// element whose frequency is equal
// to the sum of frequencies of
// other elements of the array
import java.util.*;

class GFG{

// Function to check that any element
// have frequency equal to the sum of
// frequency of other elements of the array
static boolean isFrequencyEqual(int arr[], int len)
{
    // Check that if the array length
    // is odd, Then no solution possible
    if (len % 2 == 1){
        System.out.print("No Such Element");
        return false;
    }

    // Hash-map to store the frequency
    // of elements of array
    HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();

    // Loop to find the frequency
    // of elements of array
    for (int i = 0; i < len; i++)
        if(freq.containsKey(arr[i])){
            freq.put(arr[i], freq.get(arr[i])+1);
        }
        else{
            freq.put(arr[i], 1);
        }

    // Loop to check if any element
    // of the array have frequency
    // equal to the half length
    for (int i = 0; i < len; i++){
        if (freq.containsKey(arr[i]) && freq.get(arr[i]) == len / 2){
            System.out.print(arr[i] +"\n");
            return true;
        }
    }

    System.out.print("No such element");
    return false;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 2, 3, 3, 3 };
    int n = 6;

    // Function Call
    isFrequencyEqual(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to find the
// element whose frequency is equal
// to the sum of frequencies of
// other elements of the array
using System;
using System.Collections.Generic;

class GFG{

// Function to check that any element
// have frequency equal to the sum of
// frequency of other elements of the array
static bool isFrequencyEqual(int []arr, int len)
{
    // Check that if the array length
    // is odd, Then no solution possible
    if (len % 2 == 1){
        Console.Write("No Such Element");
        return false;
    }

    // Hash-map to store the frequency
    // of elements of array
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Loop to find the frequency
    // of elements of array
    for (int i = 0; i < len; i++)
        if(freq.ContainsKey(arr[i])){
            freq[arr[i]] = freq[arr[i]]+1;
        }
        else{
            freq.Add(arr[i], 1);
        }

    // Loop to check if any element
    // of the array have frequency
    // equal to the half length
    for (int i = 0; i < len; i++){
        if (freq.ContainsKey(arr[i]) && freq[arr[i]] == len / 2){
            Console.Write(arr[i] +"\n");
            return true;
        }
    }

    Console.Write("No such element");
    return false;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 2, 3, 3, 3 };
    int n = 6;

    // Function Call
    isFrequencyEqual(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the
# element whose frequency is equal
# to the sum of frequencies of
# other elements of the array

# Function to check that any element
# have frequency equal to the sum of
# frequency of other elements of the array
def isFrequencyEqual(arr, length) :

    # Check that if the array length
    # is odd, Then no solution possible
    if (length % 2 == 1) :
        print("No Such Element");
        return False;

    # Hash-map to store the frequency
    # of elements of array
    freq = dict.fromkeys(arr, 0);

    # Loop to find the frequency
    # of elements of array
    for i in range(length) :
        freq[arr[i]] += 1;

    # Loop to check if any element
    # of the array have frequency
    # equal to the half length
    for i in range(length) :
        if (freq[arr[i]] == length / 2) :
            print(arr[i]);
            return True;

    print("No such element",end="");
    return False;

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 2, 3, 3, 3 ];
    n = 6;

    # Function Call
    isFrequencyEqual(arr, n);

# This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// Javascript program

// Function to check that any element
// have frequency equal to the sum of
// frequency of other elements of the array
function isFrequencyEqual(arr, len)
{
    // Check that if the array length
    // is odd, Then no solution possible
    if (len % 2 == 1){
        document.write("No Such Element");
        return false;
    }

    // Hash-map to store the frequency
    // of elements of array
    var freq = {};
    for (var i = 0; i < len; i++)
        freq[arr[i]] = 0;
    // Loop to find the frequency
    // of elements of array
    for (var i = 0; i < len; i++)
        freq[arr[i]]++;

    // Loop to check if any element
    // of the array have frequency
    // equal to the half length
    for (var i = 0; i < len; i++){
        if (freq[arr[i]] == len / 2){
            document.write(arr[i]);
            return true;
        }
    }

    document.write("No such element");
    return false;
}
var arr = [ 1, 2, 2, 3, 3, 3];
var n = 6;

isFrequencyEqual(arr, n);
</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N)
T3】空间复杂度: O(N)