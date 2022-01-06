# 计数数组中元素总和与其各自数字总和相等的对

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-array-with-sum-of-elements-with-the-sum-the-sum-the-digits-equal/](https://www.geeksforgeeks.org/count-pairs-in-an-array-having-sum-of-elements-with-their-respective-sum-of-digits-equal/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算数组中的[对的个数，比如(a，b)，使得 **a** 与其](https://www.geeksforgeeks.org/number-of-unique-pairs-in-an-array/)[位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)等于 **b** 与其[位数之和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)之和。

**示例:**

> **输入:** arr[] = {1，1，2，2}
> **输出:** 2
> **解释:**
> 以下是满足给定标准的配对:
> 
> 1.  **(1，1):****1+sumOfDigits(1)**和 **1+sumOfDigits(1)** 的差为 0，因此相等。
> 2.  **(2，2):****2+sumOfDigits(2)**和 **2+sumOfDigits(2)** 的差为 0，因此相等。
> 
> 因此，总对数为 2。
> 
> **输入** : arr[] = {105，96，20，2，87，96}
> **输出** t: 3
> 满足给定标准的配对如下:
> 
> 1.  **(105，96)**:**105+sumOfDigits(105)**与 **96+sumOfDigits(96)** 之差为 0，因此相等。
> 2.  **(105，96)**:**105+sumOfDigits(105)**与 **96+sumOfDigits(96)** 之差为 0，因此相等。
> 3.  **(96，96)**:**96+sumOfDigits(96)**与 **96+sumOfDigits(96)** 之差为 0，因此相等。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 0

**天真方法:**解决这个问题最简单的方法是生成给定数组的所有可能对，并对那些满足给定标准的对进行计数。检查所有配对后，打印获得的配对总数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过将元素的和及其[位数的和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)存储在[哈希映射](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/)中，然后计算相应形成的对的总数来进行优化。按照下面给出的步骤解决问题:

*   初始化一个[无序 _ 映射](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-user-defined-class-in-cpp/)、 **M** ，该映射为每个数组元素存储元素和的频率及其[位数和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并增加[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 中**(arr[I]+sumofdigts(arr[I])**的频率。
*   初始化一个变量，比如说**计数**为 **0** ，存储结果对的总计数。
*   [遍历给定的地图 **M**](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) ，如果任意元素的[频率，比如 **F** 大于等于 **2** ，那么**计数的值增加**(F *(F–1))/2。](https://www.geeksforgeeks.org/maximum-frequency-of-any-array-element-possible-by-at-most-k-increments/)
*   完成上述步骤后，打印**计数**的值作为成对计数的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of digits
// of the number N
int sumOfDigits(int N)
{
    // Stores the sum of digits
    int sum = 0;

    // If the number N is greater than 0
    while (N) {
        sum += (N % 10);
        N = N / 10;
    }

    // Return the sum
    return sum;
}

// Function to find the count of pairs
// such that arr[i] + sumOfDigits(arr[i])
// is equal to (arr[j] + sumOfDigits(arr[j])
int CountPair(int arr[], int n)
{
    // Stores the frequency of value
    // of arr[i] + sumOfDigits(arr[i])
    unordered_map<int, int> mp;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Find the value
        int val = arr[i] + sumOfDigits(arr[i]);

        // Increment the frequency
        mp[val]++;
    }

    // Stores the total count of pairs
    int count = 0;

    // Traverse the map mp
    for (auto x : mp) {

        int val = x.first;
        int times = x.second;

        // Update the count of pairs
        count += ((times * (times - 1)) / 2);
    }

    // Return the total count of pairs
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 105, 96, 20, 2, 87, 96 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << CountPair(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.*;
class GFG
{

    // Function to find the sum of digits
    // of the number N
    static int sumOfDigits(int N)
    {
        // Stores the sum of digits
        int sum = 0;

        // If the number N is greater than 0
        while (N > 0) {
            sum += (N % 10);
            N = N / 10;
        }

        // Return the sum
        return sum;
    }

    // Function to find the count of pairs
    // such that arr[i] + sumOfDigits(arr[i])
    // is equal to (arr[j] + sumOfDigits(arr[j])
    static int CountPair(int arr[], int n)
    {
        // Stores the frequency of value
        // of arr[i] + sumOfDigits(arr[i])
        HashMap<Integer, Integer> mp
            = new HashMap<Integer, Integer>();

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // Find the value
            int val = arr[i] + sumOfDigits(arr[i]);

            // Increment the frequency
            if (mp.containsKey(val)) {
                mp.put(val, mp.get(val) + 1);
            }
            else {
                mp.put(val, 1);
            }
        }

        // Stores the total count of pairs
        int count = 0;

        // Traverse the map mp
        for (Map.Entry<Integer, Integer> x :
             mp.entrySet()) {

            int val = x.getKey();
            int times = x.getValue();

            // Update the count of pairs
            count += ((times * (times - 1)) / 2);
        }

        // Return the total count of pairs
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 105, 96, 20, 2, 87, 96 };
        int N = 6;
        System.out.println(CountPair(arr, N));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the sum of digits
# of the number N
def sumOfDigits(N):
    # Stores the sum of digits
    sum = 0

    # If the number N is greater than 0
    while (N):
        sum += (N % 10)
        N = N // 10

    # Return the sum
    return sum

# Function to find the count of pairs
# such that arr[i] + sumOfDigits(arr[i])
# is equal to (arr[j] + sumOfDigits(arr[j])
def CountPair(arr, n):
    # Stores the frequency of value
    # of arr[i] + sumOfDigits(arr[i])
    mp = {}

    # Traverse the given array
    for i in range(n):
        # Find the value
        val = arr[i] + sumOfDigits(arr[i])

        # Increment the frequency
        if val in mp:
            mp[val] += 1
        else:
            mp[val] = 1

    # Stores the total count of pairs
    count = 0

    # Traverse the map mp
    for key,value in mp.items():
        val = key
        times = value

        # Update the count of pairs
        count += ((times * (times - 1)) // 2)

    # Return the total count of pairs
    return count

# Driver Code
if __name__ == '__main__':
    arr = [105, 96, 20, 2, 87, 96]
    N = len(arr)
    print(CountPair(arr, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // Function to find the sum of digits
// of the number N
static int sumOfDigits(int N)
{

    // Stores the sum of digits
    int sum = 0;

    // If the number N is greater than 0
    while (N>0) {
        sum += (N % 10);
        N = N / 10;
    }

    // Return the sum
    return sum;
}

// Function to find the count of pairs
// such that arr[i] + sumOfDigits(arr[i])
// is equal to (arr[j] + sumOfDigits(arr[j])
static int CountPair(int []arr, int n)
{
    // Stores the frequency of value
    // of arr[i] + sumOfDigits(arr[i])
    Dictionary<int, int> mp = new Dictionary<int,int>();

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Find the value
        int val = arr[i] + sumOfDigits(arr[i]);

        // Increment the frequency
        if(mp.ContainsKey(val))
         mp[val]++;
        else
         mp.Add(val,1);
    }

    // Stores the total count of pairs
    int count = 0;

    // Traverse the map mp
    foreach(KeyValuePair<int, int> entry in mp) {

        int val = entry.Key;
        int times = entry.Value;

        // Update the count of pairs
        count += ((times * (times - 1)) / 2);
    }

    // Return the total count of pairs
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 105, 96, 20, 2, 87, 96 };
    int N = arr.Length;
    Console.Write(CountPair(arr, N));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach
        // Function to find the sum of digits
        // of the number N
        function sumOfDigits(N) {
            // Stores the sum of digits
            let sum = 0;

            // If the number N is greater than 0
            while (N != 0) {
                sum = sum + (N % 10);
                N = Math.floor(N / 10);
            }

            // Return the sum
            return sum;
        }

        // Function to find the count of pairs
        // such that arr[i] + sumOfDigits(arr[i])
        // is equal to (arr[j] + sumOfDigits(arr[j])
        function CountPair(arr, n) {
            // Stores the frequency of value
            // of arr[i] + sumOfDigits(arr[i])
            let mp = new Map();

            // Traverse the given array
            for (let i = 0; i < n; i++) {

                // Find the value

                let val = arr[i] + sumOfDigits(arr[i]);
                // Increment the frequency
                if (mp.has(val)) {
                    mp.set(val, mp.get(val) + 1);
                }
                else {
                    mp.set(val, 1);
                }
            }

            // Stores the total count of pairs
            let count = 0;

            // Traverse the map mp
            for (let [key, value] of mp) {

                // Update the count of pairs

                count = count + (value * (value - 1)) / 2;
            }

            // Return the total count of pairs
            return count;
        }

        // Driver Code

        let arr = [105, 96, 20, 2, 87, 96];
        let N = arr.length;
        document.write(CountPair(arr, N))

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)