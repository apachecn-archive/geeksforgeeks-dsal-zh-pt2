# 在给定数组的相同索引处交换元素后可能的唯一数组的计数

> 原文:[https://www . geeksforgeeks . org/给定数组的同索引元素交换后的可能唯一数组计数/](https://www.geeksforgeeks.org/count-of-possible-unique-arrays-after-swapping-elements-at-same-index-of-given-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr 1【】**和**arr 2【】**具有大小为 **N.** 的不同元素，任务是在两个数组的相同**索引处交换元素后，计算可能的**组合**的总数，以便在执行操作后两个数组中没有重复的**。****

****示例:****

> ****输入:** arr1[] = {1，2，3，4}，arr2[] = {2，1，4，3}，N = 4
> **输出:** 4
> **解释:**可能的数组组合有:**
> 
> *   **{1，2，3，4}和{2，1，4，3}**
> *   **{ **2** ， **1** ，3，4}和{ **1** ， **2** ，4，3}**
> *   **{1，2， **4** ， **3** }和{2，1， **3** ， **4****
> *   **{ **2** 、 **1** 、 **4** 、 **3** }和{ **1** 、 **2** 、 **3** 、 **4****
> 
> **粗体的是交换元素。所以，组合总数= 4。**
> 
>  ****输入:** arr1[] = {3，6，5，2，1，4，7}，arr2[] = {1，7，2，4，3，5，6}，N = 7
> **输出:** 8**

****方法:**思路是每个元素迭代一次**的数组，进行一次**交换**，然后查找当前元素的交换需要多少**个额外的交换**才能使数组摆脱**个重复**。将每个不同的组合算作一个组(集合)，也就是说，对于每个组，有两种**可能进行交换或不进行交换，因此答案将是 **2 的和乘以组数****。按照以下步骤解决问题:********

1.  **创建一个**无序映射**来存储键值对中两个数组的元素**
2.  **取一个变量**计数**计算可能的组合数，也取一个向量跟踪元素**访问了**。**
3.  **迭代**地图**并检查元素是否不是**访问的**，每次创建一个**集合**并运行一个循环直到当前索引不等于 **i** 。在每次迭代中，在集合中插入地图的**当前索引**的元素，并且**更新**当前索引。将集合中的所有元素标记为已访问。**
4.  **每次迭代后，在进行分组(集合)时，**将**的计数乘以 **2** ，因为每组元素的交换或不交换有**两种可能性**。**
5.  **最后，返回**计数**。** 

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count possible combinations
// of arrays after swapping of elements
// such that there are no duplicates
// in the arrays
int possibleCombinations(int arr1[], int arr2[], int N)
{
    // Create an unordered_map
    unordered_map<int, int> mp;

    // Traverse both the arrays and
    // store the elements of arr2[]
    // in arr1[] element index in
    // the map
    for (int i = 0; i < N; i++) {
        mp[arr1[i]] = arr2[i];
    }

    // Take a variable for count of
    // possible combinations
    int count = 1;

    // Vector to keep track of already
    // swapped elements
    vector<bool> visited(N + 1, 0);
    for (int i = 1; i <= N; i++) {

        // If the element is not visited
        if (!visited[i]) {

            // Create a set
            set<int> s;

            // Variable to store the current index
            int curr_index = i;

            // Iterate a loop till curr_index
            // is equal to i
            do {

                // Insert the element in the set
                // of current index in map
                s.insert(mp[curr_index]);

                // Assign it to curr_index
                curr_index = mp[curr_index];
            } while (curr_index != i);

            // Iterate over the set and
            // mark element as visited
            for (auto it : s) {
                visited[it] = 1;
            }
            count *= 2;
        }
    }
    return count;
}

// Driver Code
int main()
{
    int arr1[] = { 3, 6, 5, 2, 1, 4, 7 };
    int arr2[] = { 1, 7, 2, 4, 3, 5, 6 };
    int N = sizeof(arr1) / sizeof(arr1[0]);

    cout << possibleCombinations(arr1, arr2, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation for the above approach
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;

class GFG
{

    // Function to count possible combinations
    // of arrays after swapping of elements
    // such that there are no duplicates
    // in the arrays
    public static int possibleCombinations(int arr1[], int arr2[], int N)
    {

        // Create an unordered_map
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Traverse both the arrays and
        // store the elements of arr2[]
        // in arr1[] element index in
        // the map
        for (int i = 0; i < N; i++) {

            mp.put(arr1[i], arr2[i]);
        }

        // Take a variable for count of
        // possible combinations
        int count = 1;

        // Vector to keep track of already
        // swapped elements
        int[] visited = new int[N + 1];
        Arrays.fill(visited, 0);
        for (int i = 1; i <= N; i++) {

            // If the element is not visited
            if (visited[i] <= 0) {

                // Create a set
                HashSet<Integer> s = new HashSet<Integer>();

                // Variable to store the current index
                int curr_index = i;

                // Iterate a loop till curr_index
                // is equal to i
                do {

                    // Insert the element in the set
                    // of current index in map
                    s.add(mp.get(curr_index));

                    // Assign it to curr_index
                    curr_index = mp.get(curr_index);
                } while (curr_index != i);

                // Iterate over the set and
                // mark element as visited
                for (int it : s) {
                    visited[it] = 1;
                }
                count *= 2;
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String args[]) {
        int arr1[] = { 3, 6, 5, 2, 1, 4, 7 };
        int arr2[] = { 1, 7, 2, 4, 3, 5, 6 };
        int N = arr1.length;

        System.out.println(possibleCombinations(arr1, arr2, N));
    }
}

// This code is contributed by gfgking.
```

## **蟒蛇 3**

```
# Python3 implementation for the above approach

# Function to count possible combinations
# of arrays after swapping of elements
# such that there are no duplicates
# in the arrays
def possibleCombinations(arr1, arr2, N) :

    # Create an unordered_map
    mp = {};

    # Traverse both the arrays and
    # store the elements of arr2[]
    # in arr1[] element index in
    # the map
    for i in range(N) :
        mp[arr1[i]] = arr2[i];

    # Take a variable for count of
    # possible combinations
    count = 1;

    # Vector to keep track of already
    # swapped elements
    visited = [0]*(N + 1);

    for i in range(1 , N + 1) :

        # If the element is not visited
        if (not visited[i]) :

            # Create a set
            s = set();

            # Variable to store the current index
            curr_index = i;

            # Iterate a loop till curr_index
            # is equal to i
            while True :

                # Insert the element in the set
                # of current index in map
                s.add(mp[curr_index]);

                # Assign it to curr_index
                curr_index = mp[curr_index];

                if (curr_index == i) :
                    break

            # Iterate over the set and
            # mark element as visited
            for it in s :
                visited[it] = 1;

            count *= 2;

    return count;

# Driver Code
if __name__ == "__main__" :

    arr1 = [ 3, 6, 5, 2, 1, 4, 7 ];
    arr2 = [ 1, 7, 2, 4, 3, 5, 6 ];
    N = len(arr1);

    print(possibleCombinations(arr1, arr2, N));

    # This code is contributed by AnkThon
```

## **C#**

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to count possible combinations
    // of arrays after swapping of elements
    // such that there are no duplicates
    // in the arrays
    public static int
    possibleCombinations(int[] arr1, int[] arr2, int N)
    {

        // Create an unordered_map
        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        // Traverse both the arrays and
        // store the elements of arr2[]
        // in arr1[] element index in
        // the map
        for (int i = 0; i < N; i++) {

            mp[arr1[i]] = arr2[i];
        }

        // Take a variable for count of
        // possible combinations
        int count = 1;

        // Vector to keep track of already
        // swapped elements
        int[] visited = new int[N + 1];

        for (int i = 1; i <= N; i++) {

            // If the element is not visited
            if (visited[i] <= 0) {

                // Create a set
                HashSet<int> s = new HashSet<int>();

                // Variable to store the current index
                int curr_index = i;

                // Iterate a loop till curr_index
                // is equal to i
                do {

                    // Insert the element in the set
                    // of current index in map
                    s.Add(mp[curr_index]);

                    // Assign it to curr_index
                    curr_index = mp[curr_index];
                } while (curr_index != i);

                // Iterate over the set and
                // mark element as visited
                foreach(int it in s) { visited[it] = 1; }
                count *= 2;
            }
        }
        return count;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr1 = { 3, 6, 5, 2, 1, 4, 7 };
        int[] arr2 = { 1, 7, 2, 4, 3, 5, 6 };
        int N = arr1.Length;

        Console.WriteLine(
            possibleCombinations(arr1, arr2, N));
    }
}

// This code is contributed by ukasp.
```

## **java 描述语言**

```
<script>

// Javascript implementation for the above approach

// Function to count possible combinations
// of arrays after swapping of elements
// such that there are no duplicates
// in the arrays
function possibleCombinations(arr1, arr2, N)
{
    // Create an unordered_map
    var mp = new Map();

    // Traverse both the arrays and
    // store the elements of arr2[]
    // in arr1[] element index in
    // the map
    for (var i = 0; i < N; i++) {
        mp.set(arr1[i], arr2[i]);
    }

    // Take a variable for count of
    // possible combinations
    var count = 1;

    // Vector to keep track of already
    // swapped elements
    var visited = Array(N + 1).fill(false);

    for (var i = 1; i <= N; i++) {

        // If the element is not visited
        if (!visited[i]) {

            // Create a set
            var s = new Set();

            // Variable to store the current index
            var curr_index = i;

            // Iterate a loop till curr_index
            // is equal to i
            do {

                // Insert the element in the set
                // of current index in map
                s.add(mp.get(curr_index));

                // Assign it to curr_index
                curr_index = mp.get(curr_index);

            } while (curr_index != i);

            // Iterate over the set and
            // mark element as visited
            for (var it of [...s]) {
                visited[it] = true;
            }
            count *= 2;
        }
    }
    return count;
}

// Driver Code
var arr1 = [3, 6, 5, 2, 1, 4, 7];
var arr2 = [1, 7, 2, 4, 3, 5, 6];
var N = arr1.length;
document.write(possibleCombinations(arr1, arr2, N));

// This code is contributed by rutvik_56.
</script>
```

****Output**

```
8
```** 

*****时间复杂度*****:**O(N<sup>2</sup>)
***辅助空间*** **:** O(N)**