# 找到最大汉明距离的旋转|设置 2

> 原文:[https://www . geeksforgeeks . org/find-a-旋转最大汉明距离-set-2/](https://www.geeksforgeeks.org/find-a-rotation-with-maximum-hamming-distance-set-2/)

给定整数数组 **arr[]** 。创建一个新阵列，它是给定阵列的旋转，并找到两个阵列之间的最大**汉明**距离。

> **汉明**两个数组或**等长字符串**之间的距离是对应字符(元素)不同**的位置数**。

**注意:**给定输入可以有多个输出。

**示例:**

> **输入:** arr[] = [1，4，1]
> 
> **输出:** 2
> 
> **解释:**最大汉明距离= 2，这个汉明距离用 4 ^ 1 ^ 1 或者 1 ^ 1 ^ 4
> 
> **输入:** arr[] = [2，4，8，0]
> 
> **输出:** 4
> 
> **说明:**最大汉明距离= 4，这个汉明距离用 4 8 0 2。所有的位置都可以被另一个数字占据。其他解决方案可以是 8 0 2 4、4 0 2 8 等。

**方法:**使用 **Hashmap** 可以高效解决这个问题。按照下面给出的步骤解决问题

*   遍历数组 **arr[]** ，将数组的值存储在 **HashMap <键中，值为>** 。根据兴趣值可以是列表< >或字符串。
*   在 hashmap 中添加值，hashMap.add(arrvalue，list)。
*   检查这种情况:
    *   当 hashMap.contains(arrValue)之后，hashmap.get(arrayValue)。追加(索引)。
*   检查散列表的大小，如果**大小== 1** 那么
    *   **最大**海明**距离= 0** 。因为所有的价值观都是一样的。
*   如果列表**大小= 1** 则为每个循环、每个键运行
    *   **最大**海明**距离= n** 。因为所有的值都不同。
*   创建一个给定数组的**大小–1**的数组，用于存储可能发生的类似事件。
*   存储完数组的所有索引后，将值存储在 **hashMap** 中。
*   对于发现的每个差异 **a += 1** 。这种差异表示在相同的位置有相同的值所需要的旋转次数。
*   找到数组中最小的值，得到**索引= >最小值**相同的**值= >最大值**海明距离。

下面是上述方法的实现:

## C++

```
// Find a rotation with maximum hamming distance
#include<bits/stdc++.h>
using namespace std;

// Function to return the min value
int getMinValue(vector<int> numbers)
{

    // var to stor the min value
    int minValue = numbers[0];

    for(int i = 1; i < numbers.size(); i++)
    {

        // Condition to check if value is
        // lesser from the minValue or not
        if (numbers[i] < minValue)
        {
            minValue = numbers[i];
        }
    }

    // Return the minValue
    return minValue;
}

// Function to get the hamming distance
int maxHammingDistance(vector<int> array)
{
    int n = array.size();
    vector<int> repetitionsOnRotations(n - 1,0);

    // Create the map to store the key value pair
    map<int, vector<int>> indexesOfElements;

    for(int i = 0; i < n; i++)
    {
        int key = array[i];

        // Take empty list of integers
        // to store the integer
        vector<int>indexes;

        if (indexesOfElements.find(key) !=
            indexesOfElements.end())
        {
            indexes = indexesOfElements[key];
        }
        else
        {
            indexes.clear();
        }

        // Add the value in list index
        indexes.push_back(i);
        indexesOfElements[key] = indexes;
    }

    // Run the for loop and get the
    // value from hash map one at a time
    for(auto x : indexesOfElements)
    {
        vector<int> indexes = x.second;

        for(int i = 0; i < indexes.size() - 1; i++)
        {
            for(int j = i + 1; j < indexes.size(); j++)
            {

                // Store the diff into the variable
                int diff = indexes[i] - indexes[j];

                // Check the condition if diff
                // is less then zero or not
                if (diff < 0)
                {
                    repetitionsOnRotations[-diff - 1] += 1;
                    diff = n + diff;
                }
                repetitionsOnRotations += 1;
            }
        }
    }

    // Return the hamming distance
    return n - getMinValue(repetitionsOnRotations);
}

// Driver code
int main()
{

    // Example 1
    vector<int> array{ 1, 4, 1 };
    int result1 = maxHammingDistance(array);
    cout << result1 << endl;

    // Example 2
    vector<int> array2{ 2, 4, 8, 0 };
    int result2 = maxHammingDistance(array2);
    cout << result2 << endl;
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Find a rotation with maximum hamming distance

import java.io.*;
import java.util.*;

class GFG {

    // Function to return the min value
    public static int getMinValue(int[] numbers)
    {

        // var to stor the min value
        int minValue = numbers[0];

        for (int i = 1; i < numbers.length; i++) {

            // Condition to check if value is
            // lesser from the minValue or not
            if (numbers[i] < minValue) {
                minValue = numbers[i];
            }
        }

        // Return the minValue
        return minValue;
    }

    // Function to get the hamming distance
    public static int maxHammingDistance(int[] array)
    {

        int n = array.length;
        int[] repetitionsOnRotations = new int[n - 1];

        // Create the map to store the key value pair
        Map<Integer, List<Integer> > indexesOfElements
            = new HashMap<>();

        for (int i = 0; i < n; i++) {

            int key = array[i];

            // Take empty list of integers
            // to store the integer
            List<Integer> indexes = null;

            if (indexesOfElements.containsKey(key)) {
                indexes = indexesOfElements.get(key);
            }
            else {
                indexes = new ArrayList<>();
            }
            // Add the value in list index
            indexes.add(i);
            indexesOfElements.put(key, indexes);
        }

        // Run the for loop and get the
        // value from hash map one at a time
        for (Map.Entry<Integer, List<Integer> > keys :
             indexesOfElements.entrySet()) {

            List<Integer> indexes = keys.getValue();

            for (int i = 0; i < indexes.size() - 1; i++) {
                for (int j = i + 1; j < indexes.size(); j++) {

                    // Store the diff into the variable
                    int diff
                        = indexes.get(i) - indexes.get(j);

                    // Check the condition if diff
                    // is less then zero or not
                    if (diff < 0) {
                        repetitionsOnRotations[(-diff) - 1] += 1;
                        diff = n + diff;
                    }
                    repetitionsOnRotations += 1;
                }
            }
        }

        // Return the hamming distance
        return n - (getMinValue(repetitionsOnRotations));
    }

    // Driver code
    public static void main(String[] args)
    {

        // Example 1
        int[] array = { 1, 4, 1 };
        int result1 = GFG.maxHammingDistance(array);
        System.out.println(result1);

        // Example 2
        int[] array2 = { 2, 4, 8, 0 };
        int result2 = GFG.maxHammingDistance(array2);
        System.out.println(result2);
    }
}
```

## 蟒蛇 3

```
# Find a rotation with maximum hamming distance

# Function to return the min value
def getMinValue(numbers):

    # var to stor the min value
    minValue = numbers[0]

    for i in range(1, len(numbers)):

        # Condition to check if value is
        # lesser from the minValue or not
        if (numbers[i] < minValue):
            minValue = numbers[i]

    # Return the minValue
    return minValue

# Function to get the hamming distance
def maxHammingDistance(array):
    n = len(array)
    repetitionsOnRotations = [0] * (n - 1)

    # Create the map to store the key value pair
    indexesOfElements = {}

    for i in range(n):
        key = array[i]

        # Take empty list of integers
        # to store the integer
        indexes = []

        if (key in indexesOfElements):
            indexes = indexesOfElements[key]
        else:
            indexes = []

        # Add the value in list index
        indexes.append(i)
        indexesOfElements[key] = indexes

    # Run the for loop and get the
    # value from hash map one at a time
    for indexes in indexesOfElements.values():

        for i in range(len(indexes) - 1):
            for j in range(i + 1, len(indexes)):

                # Store the diff into the variable
                diff = indexes[i] - indexes[j]

                # Check the condition if diff
                # is less then zero or not
                if (diff < 0):
                    repetitionsOnRotations[-diff - 1] += 1
                    diff = n + diff

                repetitionsOnRotations += 1

    # Return the hamming distance
    return n - getMinValue(repetitionsOnRotations)

# Driver code

# Example 1
array = [1, 4, 1]
result1 = maxHammingDistance(array)
print(result1)

# Example 2
array2 = [2, 4, 8, 0]
result2 = maxHammingDistance(array2)
print(result2)

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// Find a rotation with maximum hamming distance
using System;
using System.Collections.Generic;

class GFG{

// Function to return the min value
public static int getMinValue(int[] numbers)
{

    // var to stor the min value
    int minValue = numbers[0];

    for(int i = 1; i < numbers.Length; i++)
    {

        // Condition to check if value is
        // lesser from the minValue or not
        if (numbers[i] < minValue)
        {
            minValue = numbers[i];
        }
    }

    // Return the minValue
    return minValue;
}

// Function to get the hamming distance
public static int maxHammingDistance(int[] array)
{
    int n = array.Length;
    int[] repetitionsOnRotations = new int[n - 1];

    // Create the map to store the key value pair
    Dictionary<int,
          List<int>> indexesOfElements = new Dictionary<int,
                                                   List<int>>();

    for(int i = 0; i < n; i++)
    {
        int key = array[i];

        // Take empty list of integers
        // to store the integer
        List<int> indexes = null;

        if (indexesOfElements.ContainsKey(key))
        {
            indexes = indexesOfElements[key];
        }
        else
        {
            indexes = new List<int>();
        }

        // Add the value in list index
        indexes.Add(i);
        if (!indexesOfElements.ContainsKey(key))
            indexesOfElements.Add(key, indexes);
    }

    // Run the for loop and get the
    // value from hash map one at a time
    foreach(KeyValuePair<int,
                    List<int>> keys in indexesOfElements)
    {
        List<int> indexes = keys.Value;

        for(int i = 0; i < indexes.Count - 1; i++)
        {
            for(int j = i + 1; j < indexes.Count; j++)
            {

                // Store the diff into the variable
                int diff = indexes[i] - indexes[j];

                // Check the condition if diff
                // is less then zero or not
                if (diff < 0)
                {
                    repetitionsOnRotations[(-diff) - 1] += 1;
                    diff = n + diff;
                }
                repetitionsOnRotations += 1;
            }
        }
    }

    // Return the hamming distance
    return n - (getMinValue(repetitionsOnRotations));
}

// Driver code
public static void Main(String[] args)
{

    // Example 1
    int[] array = { 1, 4, 1 };
    int result1 = GFG.maxHammingDistance(array);
    Console.WriteLine(result1);

    // Example 2
    int[] array2 = { 2, 4, 8, 0 };
    int result2 = GFG.maxHammingDistance(array2);
    Console.WriteLine(result2);
}
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>

// Find a rotation with maximum hamming distance

// Function to return the min value
function getMinValue(numbers)
{

    // var to stor the min value
    let minValue = numbers[0];

    for(let i = 1; i < numbers.length; i++)
    {

        // Condition to check if value is
        // lesser from the minValue or not
        if (numbers[i] < minValue)
        {
            minValue = numbers[i];
        }
    }

    // Return the minValue
    return minValue;
}

// Function to get the hamming distance
function maxHammingDistance(array)
{
    let n = array.length;
    let repetitionsOnRotations = new Array(n - 1).fill(0);

    // Create the map to store the key value pair
    let indexesOfElements = new Map();

    for(let i = 0; i < n; i++)
    {
        let key = array[i];

        // Take empty list of integers
        // to store the integer
        let indexes = [];

        if (indexesOfElements.has(key))
        {
            indexes = indexesOfElements.get(key);
        }
        else
        {
            indexes = [];
        }

        // Add the value in list index
        indexes.push(i);
        indexesOfElements.set(key, indexes);
    }

    // Run the for loop and get the
    // value from hash map one at a time
    for(let keys of indexesOfElements)
    {
        let indexes = keys[1];

        for(let i = 0; i < indexes.length - 1; i++)
        {
            for(let j = i + 1; j < indexes.length; j++)
            {

                // Store the diff into the variable
                let diff = indexes[i] - indexes[j];

                // Check the condition if diff
                // is less then zero or not
                if (diff < 0)
                {
                    repetitionsOnRotations[-diff - 1] += 1;
                    diff = n + diff;
                }
                repetitionsOnRotations += 1;
            }
        }
    }

    // Return the hamming distance
    return n - getMinValue(repetitionsOnRotations);
}

// Driver code

// Example 1
let array = [ 1, 4, 1 ];
let result1 = maxHammingDistance(array);
document.write(result1 + "<br>");

// Example 2
let array2 = [ 2, 4, 8, 0 ];
let result2 = maxHammingDistance(array2);
document.write(result2);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2
4
```

***时间复杂度:** O(N)*